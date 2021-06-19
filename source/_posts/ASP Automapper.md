---

title: ASP Pagination Implementation Based On Entity Framework
date: 06/16/2021
updated: 
tags: 
  - notes
  - Pagination
  - Entity Framework
categories: ASP
keywords: 
description: 
top_img: 
comments: 
cover: 
toc: 
toc_number: 
copyright:
copyright_author: Shiqi Zhang
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

Introduction

Define paginated list inhered from **List**, having the property **PageIndex** (The page number) ,**TotalPages** (Count/pageSize), ***TotalCount***(total item count), this one is not necessary becuase the count is accessible from ```List.Count``` Therefore, in order to get the next page, you need to send the next pageIndex to controller(PageIndex + 1). The page size is set to 30 by default. The page size is option parameter for controller. The GetPaged method is a static method to get paged list by **skipping** the number of page number. 

```c#
public class PaginatedList<T> : List<T> where T: class
    {
        public PaginatedList(List<T> items, int count, int page, int pageSize)
        {
            PageIndex = page;
            TotalPages = (int) Math.Ceiling(count / (double) pageSize);
            TotalCount = count;
            AddRange(items);
        }

        public PaginatedList()
        {
            
        }
        public int PageIndex { get; set; }
        public int TotalPages { get; set; }
        public int TotalCount { get; set; }
        public bool HasPreviousPage => PageIndex > 1;
        public bool HasNextPage => PageIndex < TotalPages;

        public static async Task<PaginatedList<T>> GetPaged(
            IQueryable<T> source, int pageIndex, int pageSize,
            Func<IQueryable<T>, IOrderedQueryable<T>> orderedQuery = null,
            Expression<Func<T, bool>> filter = null, 
            params Expression<Func<T, object>>[] includes)
        {
            // source query which implemented IQuerable
            var query = source;
            
            // A expression tree accepts a lambda expression
            if (filter != null) query = query.Where(filter);
            
            // orderedQuery is a delegate that accept a IQueryable as parameter and outputs IOrderedQueryable.
            // In this example, query is a parameter, executes the lambda expression function
           // orderQuery = rev => rev.OrderByDescending(r => r.Rating)
            if (orderedQuery != null) query = orderedQuery(query);
            
            //Assign Lambda expressions Includes to Expression Tree
            if (includes != null)
                foreach (Expression<Func<T, object>> navigationProperty in includes)
                    query = query.Include(navigationProperty);

            var count = await query.CountAsync();
            var items = await query.Skip((pageIndex - 1) * pageSize).Take(pageSize).ToListAsync();
            return new PaginatedList<T>(items, count, pageIndex, pageSize);
        }
    }
```

The PagedResultSet is a simplfied class to store IEnumberables, I don't know the other use, let me know if you had some ideas. 

```c#
public class PagedResultSet<TEntity> where TEntity : class
    {
        public PagedResultSet(IEnumerable<TEntity> data, int pageIndex, int pageSize, int count)
        {
            PageIndex = pageIndex;
            PageSize = pageSize;
            Count = count;
            Data = data;
            TotalPages = (int) Math.Ceiling(count / (double) pageSize);
        }

        public int PageIndex { get; }
        public int PageSize { get; }
        public int TotalPages { get; }
        public long Count { get; }
        public IEnumerable<TEntity> Data { get; }
    }
```

Every Repository should implement the GetPagedData method, which is simply invoke the PaginatedList's static method with parameters, page, pageSize, orderedQuery, filter, includes. 

```c#
public interface IAsyncRepository<T> where T : class
    {
        ...
        
            Task<PaginatedList<T>> GetPagedData(int pageIndex, int pageSize, Func<IQueryable<T>, IOrderedQueryable<T>> orderedQuery = null, Expression<Func<T, bool>> filter = null, params Expression<Func<T, object>>[] includes);
    }
```

 GetPagedData Method requires no source since EfRepository class has DbContext for entity class T

The base Repository class:


```c#
public class EfRepository<T> : IAsyncRepository<T> where T : class
    {
        protected readonly MovieShopDbContext _dbContext;

        public EfRepository(MovieShopDbContext dbContext)
        {
            _dbContext = dbContext;
        }


        public virtual async Task<PaginatedList<T>> GetPagedData(int page = 1, int pageSize = 25,
            Func<IQueryable<T>, IOrderedQueryable<T>> orderedQuery
                = null, Expression<Func<T, bool>> filter = null, params Expression<Func<T, object>>[] includes)
        {
            var pagedList =
                await PaginatedList<T>.GetPaged(_dbContext.Set<T>(), page, pageSize, orderedQuery, filter, includes);
            return pagedList;
        }
    }
```

The service's class gets different paged result sets based on the bussiness logic. 


```c#
   public interface IMovieService
    {
        Task<PagedResultSet<MovieResponseModel>> GetMoviesByPagination(int pageSize = 20, int page = 1, string title = "");
        Task<PagedResultSet<MovieResponseModel>> GetAllMoviePurchasesByPagination(int pageSize = 20, int page = 1);
        Task<PagedResultSet<MovieResponseModel>> GetAllPurchasesByMovieId(int movieId);
        Task<PaginatedList<MovieResponseModel>> GetMoviesByGenre(int genreId, int pageSize = 25, int page = 1);
        ...
    }
```

- The ```mov => mov.OrderBy(m => m.Title)``` assigned ```IOrderedQueryable<T> orderedQuery = null```

-  ```if (!string.IsNullOrEmpty(title)) filterExpression = movie => title != null && movie.Title.Contains(title);``` if the title is not null or empty, assigned ```Expression<Func<T, bool>> filter = null``` with filterExpression. 

  For the example,```_reviewRepository.GetPagedData(1, 25, rev => rev.OrderByDescending(r => r.Rating), filterExpression, review => review.Movie);``` ```review => review.Movie``` is a Include expression tree having delegate Func<T,object> to let ```DbSet\<Review\>().Include(Func<T,object>)```.

  *See C# Core I: LINQ for definition of ExpressionTree*


```c#
 public class MovieService : IMovieService
    {
        private readonly IAsyncRepository<Favorite> _favoriteRepository;
        private readonly IAsyncRepository<Genre> _genreRepository;
        private readonly IMapper _mapper;
        private readonly IMovieRepository _movieRepository;
        private readonly IPurchaseRepository _purchaseRepository;
        private readonly IAsyncRepository<Review> _reviewRepository;

        public MovieService(IMovieRepository movieRepository, IMapper mapper, IPurchaseRepository purchaseRepository,
            IAsyncRepository<Favorite> favoriteRepository, IAsyncRepository<Review> reviewRepository,
            IAsyncRepository<Genre> genreRepository)
        {
            _movieRepository = movieRepository;
            _mapper = mapper;
            _purchaseRepository = purchaseRepository;
            _favoriteRepository = favoriteRepository;
            _reviewRepository = reviewRepository;
            _genreRepository = genreRepository;
        }

        public async Task<PagedResultSet<MovieResponseModel>> GetMoviesByPagination(
            int pageSize = 20, int pageIndex = 0, string title = "")
        {
            Expression<Func<Movie, bool>> filterExpression = null;
            if (!string.IsNullOrEmpty(title)) filterExpression = movie => title != null && movie.Title.Contains(title);

            var pagedMovies = await _movieRepository.GetPagedData(pageIndex, pageSize, mov => mov.OrderBy(m => m.Title),
                filterExpression);
            var movies =
                new PagedResultSet<MovieResponseModel>(_mapper.Map<List<MovieResponseModel>>(pagedMovies),
                    pagedMovies.PageIndex,
                    pageSize, pagedMovies.TotalCount);
            return movies;
        }

        public async Task<PagedResultSet<MovieResponseModel>> GetAllMoviePurchasesByPagination(int pageSize = 50,
            int page = 0)
        {
            var totalPurchases = await _purchaseRepository.GetCountAsync();
            var purchases = await _purchaseRepository.GetAllPurchases(pageSize, page);

            var data = _mapper.Map<List<MovieResponseModel>>(purchases);
            var purchasedMovies = new PagedResultSet<MovieResponseModel>(data, page, pageSize, totalPurchases);
            return purchasedMovies;
        }


        public async Task<PaginatedList<MovieResponseModel>> GetMoviesByGenre(int genreId, int pageSize = 30,
            int page = 1)
        {
            var pagedMovies = await _movieRepository.GetMoviesByGenre(genreId, pageSize, page);
            var data = _mapper.Map<PaginatedList<MovieResponseModel>>(pagedMovies);
            var movies = new PaginatedList<MovieResponseModel>(data, pagedMovies.TotalCount, page, pageSize);
            return movies;
        }

        public async Task<MovieDetailsResponseModel> GetMovieAsync(int id)
        {
            var movie = await _movieRepository.GetByIdAsync(id);
            if (movie == null) throw new NotFoundException("Movie", id);
            var favoritesCount = await _favoriteRepository.GetCountAsync(f => f.MovieId == id);
            var response = _mapper.Map<MovieDetailsResponseModel>(movie);
            response.FavoritesCount = favoritesCount;
            return response;
        }

        public async Task<IEnumerable<ReviewMovieResponseModel>> GetReviewsForMovie(int id)
        {
            Expression<Func<Review, bool>> filterExpression = review => review.MovieId == id;

            var reviews = await _reviewRepository.GetPagedData(1, 25, rev => rev.OrderByDescending(r => r.Rating),
                filterExpression, review => review.Movie);

            var response = _mapper.Map<IEnumerable<ReviewMovieResponseModel>>(reviews);
            return response;
        }

        public async Task<int> GetMoviesCount(string title = "")
        {
            if (string.IsNullOrEmpty(title)) return await _movieRepository.GetCountAsync();
            return await _movieRepository.GetCountAsync(m => m.Title.Contains(title));
        }

    }
```

The controller acquires the PagedList from services then assign it to the View.

```
 public class HomeController : Controller
    {
        private readonly ILogger<HomeController> _logger;
        private readonly IMovieService _movieService;

        public HomeController(ILogger<HomeController> logger, IMovieService movieService)
        {
            _logger = logger;
            _movieService = movieService;
        }

        public async Task<IActionResult> Genre(int id, int pageSize = 30, int pageNumber = 1)
        {
            var movies = await _movieService.GetMoviesByGenre(id, pageSize, pageNumber);
            return View("PagedIndex", movies);
        }
    }
```

In PagedIndex.cshtml: 

```<asp-route-pageNumber>``` is sent to the controller and the parameter name controller receives should be pageNumber by convention i guess? Correct me if i am wrong. 

```@{
    var prevDisabled = !Model.HasPreviousPage ? "disabled" : "";
    var nextDisabled = !Model.HasNextPage ? "disabled" : "";
    ...
    <a asp-action="Genre" asp-route-pageNumber="@(Model.PageIndex - 1)" class="btn btn-primary @prevDisabled"> 
            Previous
    </a>
```

```html
@model ApplicationCore.Helpers.PaginatedList<ApplicationCore.Models.MovieResponseModel>

<div class="rounded">
    <div class="container-fluid bg-light">
        <div class="row">
            @foreach (var movie in Model)
            {
                <div class="col-6 col-lg-3 col-sm-4 col-xl-2">
                    @*<partial name="MovieCard" model="movie"/>*@
                    @await Html.PartialAsync("_MovieCard", movie)
                </div>
            }
        </div>
    </div>
</div>

@{
    var prevDisabled = !Model.HasPreviousPage ? "disabled" : "";
    var nextDisabled = !Model.HasNextPage ? "disabled" : "";
}

<a asp-action="Genre"
   asp-route-pageNumber="@(Model.PageIndex - 1)"
   class="btn btn-primary @prevDisabled">
    Previous
</a>
<a asp-action="Genre"
   asp-route-pageNumber="@(Model.PageIndex + 1)"
   class="btn btn-primary @nextDisabled">
    Next
</a>
```





```c#



public virtual async Task<T> GetByIdWithIncludesAsync(int id,Expression<Func<T, bool>> filter, Func<IQueryable<T>, IIncludableQueryable<T, object>> include = null)

        {
            var query = _dbContext.Set<T>().AsQueryable();

            if (include != null)
                query = include(query);
            
            if (filter != null)
                query = query.Where(filter);

            return await query.SingleOrDefaultAsync();
        }


 public async Task<Movie> GetMovieWithGenresAndCast(int id)
        {
            
            var movie = GetByIdWithIncludesAsync(id: id, filter: m => m.Id == id, 
                include:m =>m
                    .Include( m=>m.MovieCasts)
                    .ThenInclude(mc=>mc.Cast)
                    .Include(m=>m.MovieGenres)
                    .ThenInclude(mg=>mg.Genre) );
            return await movie;
        }

   public async Task<MovieDetailResponseModel> GetMovieDetailsById(int id)
        {
            var movie = await _movieRepository.GetMovieWithGenresAndCast(id);
            var movieDetailResponseModel = _mapper.Map<Movie,MovieDetailResponseModel>(movie);
            return movieDetailResponseModel;
        }



   CreateMap<Movie, MovieDetailResponseModel>()
                    .ForMember(md => md.Casts, opt => opt.MapFrom(src => GetCasts(src)))
                    .ForMember(md => md.Genres, opt => opt.MapFrom(src => GetGenres(src.MovieGenres)));

           


  private static List<MovieDetailResponseModel.CastResponseModel> GetCasts(Movie movie)
        {
            IEnumerable<MovieCast> srcMovieCasts = movie.MovieCasts;
            var movieDetailResponseModel = new MovieDetailResponseModel
            {
                Casts = new List<MovieDetailResponseModel.CastResponseModel>(),
                
            };
            foreach (var cast in srcMovieCasts)
            {
                movieDetailResponseModel.Casts.Add(new MovieDetailResponseModel.CastResponseModel
                {
                    Id = cast.CastId,
                    Gender = cast.Cast.Gender,
                    Name = cast.Cast.Name,
                    ProfilePath = cast.Cast.ProfilePath,
                    TmdbUrl = cast.Cast.TmdbUrl,
                    Character = cast.Character
                });
            }
            
            return movieDetailResponseModel.Casts;
        }
        
        private static List<MovieDetailResponseModel.GenreResponseModel> GetGenres(IEnumerable<MovieGenre> srcMovieGenres)
        {
            var movieDetailResponseModel = new MovieDetailResponseModel
            {
                Genres = new List<MovieDetailResponseModel.GenreResponseModel>(),
                
            };
            foreach (var genre in srcMovieGenres)
                movieDetailResponseModel.Genres.Add(new MovieDetailResponseModel.GenreResponseModel
                {
                    Id = genre.GenreId,
                   
                    Name = genre.Genre.Name,
                    
                });

            return movieDetailResponseModel.Genres;
        }
```

