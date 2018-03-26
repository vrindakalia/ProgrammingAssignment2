### Caching the Inverse of  Matrix

The first function, `makeCacheMatrix` creates a special "matrix, which is
really a list containing a function to

1.  set the value of the matrix
2.  get the value of the matrix
3.  set the value of the inverse of the matrix
4.  get the value of the inverse of the matrix

<!-- -->

    makeCacheMatrix <- function(x = matrix()) {
        i <- NULL
        set <- function (z){
                x <<- z
                i <<- NULL
        }
        get <- function() x
        setinv <- function(solve) i <<- solve
        getinv <- function() i
        list(set = set, get = get, setinv = setinv, getinv = getinv)
        }

The following function calculates the inverse of the special "matrix"
created with the above function. However, it first checks to see if the
inverse has already been calculated. If so, it `get`s the inverse from the
cache and skips the computation. Otherwise, it calculates the inverse of
the data and sets the value of the inverse in the cache via the `setinv`
function.

    cacheSolve <- function(x, ...) {
        i <- x$getinv()
        if(!is.null(i)){ #Checks if inverse has already been computed
                message("using cached data")
                return(i) #Returns cached inverse
        }
        
        data <- x$get()
        i <- solve(data,...) #Computes inverse
        x$setinv(i) #Saves inverse to be retrieved later
        i
        }


