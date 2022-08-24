# Assignment-Caching-the-Inverse-of-a-Matrix
Assignment: Caching the Inverse of a Matrix
Matrix inversion is usually a costly computation and there may be some benefit to caching the inverse of a matrix rather than computing it repeatedly (there are also alternatives to matrix inversion that we will not discuss here). 

**makeCacheMatrix**: This function creates a special "matrix" object that can cache its inverse.

```{r}
makeCacheMatrix <- function(x = numeric()) {
        m <- NULL
        set <- function(y) {
                x <<- y
                m <<- NULL
        }
        get <- function() x
        setinverse <- function(inverse) m <<- inverse
        getinverse <- function() m
        list(set = set, get = get,
             setinverse = setinverse,
             getinverse =getinverse)
}
```

**cacheSolve**: This function computes the inverse of the special "matrix" returned by makeCacheMatrix above. If the inverse has already been calculated (and the matrix has not changed), then cacheSolve should retrieve the inverse from the cache.

```{r}
cacheSolve <- function(x, ...) {
        m <- x$getinverse()
        if(!is.null(m)) {
                message("getting cached data")
                return(m)
        }
        data <- x$get()
        m <- solve(data, ...)
        x$setinverse(m)
        m
}
```

Computing the inverse of a square matrix can be done with the solve function in R. For example, if X is a square invertible matrix, then **solve(X)** returns its inverse.

```{r}
my_matrix <- matrix(c(3,0,0,0,2,0,0,0,6),3,3)
A<-makeCacheMatrix(my_matrix)
cacheSolve(A)

```
