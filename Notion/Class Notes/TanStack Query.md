Created: December 7, 2023 9:12 AM
Class: Agility IO InternShip
Type: Front-end
Materials: https://tanstack.com/query/v3/docs/react/overview
Reviewed: No
Edited: May 10, 2025 2:46 PM

# Overview

<aside>
💡 **React Query** is often described as the missing data-fetching library for **React**, but in more technical terms, it makes **`*fetching*`, `*caching*`, `*synchronizing*` and `u*pdating server state*`** in your React applications a breeze.

</aside>

## Installation

```bash
pnpm i react-query
# or
yarn add react-query
```

<aside>
📌 React Query is compatible with **React v16.8+** and works with **ReactDOM** and **React Native**.

</aside>

## Quick Start

This example very briefly illustrates the 3 core concepts of React Query:

- [**Queries**](TanStack%20Query.md)
- [**Mutations**](TanStack%20Query.md)
- [**Query Invalidation**](TanStack%20Query.md)

```jsx
import {
  useQuery,
  useMutation,
  useQueryClient,
  QueryClient,
  QueryClientProvider,
} from 'react-query'
import { getTodos, postTodo } from '../my-api'

// Create a client
const queryClient = new QueryClient()

function App() {
  return (
    // Provide the client to your App
    <QueryClientProvider client={queryClient}>
      <Todos />
    </QueryClientProvider>
  )
}

function Todos() {
  // Access the client
  const queryClient = useQueryClient()

  // Queries
  const query = useQuery('todos', getTodos)

  // Mutations
  const mutation = useMutation(postTodo, {
    onSuccess: () => {
      // Invalidate and refetch
      queryClient.invalidateQueries('todos')
    },
  })

  return (
    <div>
      <ul>
        {query.data.map(todo => (
          <li key={todo.id}>{todo.title}</li>
        ))}
      </ul>

      <button
        onClick={() => {
          mutation.mutate({
            id: Date.now(),
            title: 'Do Laundry',
          })
        }}
      >
        Add Todo
      </button>
    </div>
  )
}

render(<App />, document.getElementById('root'))
```

<aside>
📌 React Query is configured with aggressive but sane defaults.

</aside>

[Important Defaults | TanStack Query Docs](https://tanstack.com/query/v3/docs/react/guides/important-defaults)

## Queries

A query is a declarative dependency on an asynchronous source of data that is tied to a ***unique key**.* A query can be used with any Promise based method (including **GET** and **POST** methods) to fetch data from a server.

```jsx
import { useQuery } from 'react-query'

function App() {
  const { isLoading, isError, data, error } = useQuery('todos', fetchTodoList)
}
```

### Query Keys

At its core, **React Query** manages query caching for you based on *query keys*. Query keys can be as simple as a *string*, or as complex as an *array* of many strings and nested objects.

### Query Functions

A query function can be literally any function that ***returns a promise**.* The promise that is returned should either **resolve the data** or **throw an error**.

### Parallel Queries

When the number of parallel queries does not change, there is **no extra effort** to use parallel queries. Just use any number of React Query's **`useQuery`** and **`useInfiniteQuery`** hooks side-by-side!

```jsx
function App () {
  // The following queries will execute in parallel
  const usersQuery = useQuery('users', fetchUsers)
  const teamsQuery = useQuery('teams', fetchTeams)
  const projectsQuery = useQuery('projects', fetchProjects)
  ...
}
```

### Dynamic Parallel Queries with `useQueries`

```jsx
function App({ users }) {
  const userQueries = useQueries(
    users.map(user => {
      return {
        queryKey: ['user', user.id],
        queryFn: () => fetchUserById(user.id),
      }
    })
  )
}
```

### Dependent Queries

Dependent (or serial) queries depend on previous ones to finish before they can execute. To achieve this, it's as easy as using the **`enabled`** option to tell a query when it is ready to run

```jsx
// Get the user
const { data: user } = useQuery(['user', email], getUserByEmail)

const userId = user?.id

// Then get the user's projects
const { isIdle, data: projects } = useQuery(
  ['projects', userId],
  getProjectsByUser,
  {
    // The query will not execute until the userId exists
    enabled: !!userId,
  }
)

// isIdle will be `true` until `enabled` is true and the query begins to fetch.
// It will then go to the `isLoading` stage and hopefully the `isSuccess` stage :)
```

### Query Retries

When a **`useQuery`** query fails (the query function throws an error), **React Query** will automatically retry the query if that query's request has not reached the max number of consecutive retries (defaults to **`3`**) or a function is provided to determine if a retry is allowed.

- Setting **`retry = false`** will disable retries.
- Setting **`retry = 6`** will retry failing requests 6 times before showing the final error thrown by the function.
- Setting **`retry = true`** will infinitely retry failing requests.
- Setting **`retry = (failureCount, error) => ...`** allows for custom logic based on why the request failed.

### Paginated / Lagged Queries

Rendering paginated data is a very common **UI** pattern and in **React Query**, it "just works" by including the page information in the *query key*

```jsx
const result = useQuery(['projects', page], fetchProjects)
```

[Paginated / Lagged Queries | TanStack Query Docs](https://tanstack.com/query/v3/docs/react/guides/paginated-queries#better-paginated-queries-with-keeppreviousdata)

### Infinite Queries

Rendering lists that can additively **load more** data onto an existing set of data or **infinite scroll** is also a very common **UI** pattern. **React Query** supports a useful version of **`useQuery`** called **`useInfiniteQuery`** for querying these types of lists.

[Infinite Queries | TanStack Query Docs](https://tanstack.com/query/v3/docs/react/guides/infinite-queries)

```jsx
import { useInfiniteQuery } from 'react-query'

function Projects() {
  const fetchProjects = ({ pageParam = 0 }) =>
    fetch('/api/projects?cursor=' + pageParam)

  const {
    data,
    error,
    fetchNextPage,
    hasNextPage,
    isFetching,
    isFetchingNextPage,
    status,
  } = useInfiniteQuery('projects', fetchProjects, {
    getNextPageParam: (lastPage, pages) => lastPage.nextCursor,
  })
	...
}
```

### Initial Query Data

[Initial Query Data | TanStack Query Docs](https://tanstack.com/query/v3/docs/react/guides/initial-query-data)

### Placeholder Query Data

[Placeholder Query Data | TanStack Query Docs](https://tanstack.com/query/v3/docs/react/guides/placeholder-query-data)

### Prefetching

[Prefetching | TanStack Query Docs](https://tanstack.com/query/v3/docs/react/guides/prefetching)

## Mutations

Unlike queries, mutations are typically used to *create/update/delete* data or perform server side-effects. For this purpose, **React Query** exports a **`useMutation`** hook.

A mutation can only be in one of the following states at any given moment:

- **`isIdle`** or **`status === 'idle'`** - The mutation is currently idle or in a fresh/reset state
- **`isLoading`** or **`status === 'loading'`** - The mutation is currently running
- **`isError`** or **`status === 'error'`** - The mutation encountered an error
- **`isSuccess`** or **`status === 'success'`** - The mutation was successful and mutation data is available

Beyond those primary states, more information is available depending on the state of the mutation:

- **`error`** - If the mutation is in an **`error`** state, the error is available via the **`error`** property.
- **`data`** - If the mutation is in a **`success`** state, the data is available via the **`data`** property.

```jsx
const CreateTodo = () => {
  const mutation = useMutation(formData => {
    return fetch('/api', formData)
  })

  const onSubmit = event => {
    event.preventDefault()
    mutation.mutate(new FormData(event.target))
  }

  return <form onSubmit={onSubmit}>...</form>
}
```

### Resetting Mutation State

t's sometimes the case that you need to clear the **`error`** or **`data`** of a mutation request.

```jsx
const CreateTodo = () => {
  const [title, setTitle] = useState('')
  const mutation = useMutation(createTodo)

  const onCreateTodo = e => {
    e.preventDefault()
    mutation.mutate({ title })
  }

  return (
    <form onSubmit={onCreateTodo}>
      {mutation.error && (
        <h5 onClick={() => mutation.reset()}>{mutation.error}</h5>
      )}
      <input
        type="text"
        value={title}
        onChange={e => setTitle(e.target.value)}
      />
      <br />
      <button type="submit">Create Todo</button>
    </form>
  )
}
```

### Mutation Side Effect

**`useMutation`** comes with some helper options that allow quick and easy side-effects at any stage during the mutation lifecycle.

```jsx
useMutation(addTodo, {
  onMutate: variables => {
    // A mutation is about to happen!

    // Optionally return a context containing data to use when for example rolling back
    return { id: 1 }
  },
  onError: (error, variables, context) => {
    // An error happened!
    console.log(`rolling back optimistic update with id ${context.id}`)
  },
  onSuccess: (data, variables, context) => {
    // Boom baby!
  },
  onSettled: (data, error, variables, context) => {
    // Error or success... doesn't matter!
  },
})
```

### Consecutive mutations

There is a slight difference in handling **`onSuccess`**, **`onError`** and **`onSettled`** callbacks when it comes to **consecutive mutations**. When passed to the **`mutate`** function, they will be fired up only *once* and only if the component is still mounted. This is due to the fact that mutation observer is removed and resubscribed every time when the **`mutate`** function is called.

<aside>
<img src="https://www.notion.so/icons/exclamation-mark_red.svg" alt="https://www.notion.so/icons/exclamation-mark_red.svg" width="40px" /> ***Be aware that most likely, `mutationFn` passed to `useMutation` is ansynchronous. In that case, the order in which mutations are fulfilled may differ from the order of `mutate` function calls.***

</aside>

```jsx
useMutation(addTodo, {
  onSuccess: (data, error, variables, context) => {
    // Will be called 3 times
  },
})

['Todo 1', 'Todo 2', 'Todo 3'].forEach((todo) => {
  mutate(todo, {
    onSuccess: (data, error, variables, context) => {
      // Will execute only once, for the last mutation (Todo 3),
      // regardless which mutation resolves first 
    },
  })
})
```

### Persist mutations

Mutations can be persisted to storage if needed and resumed at a later point.

[Mutations | TanStack Query Docs](https://tanstack.com/query/v3/docs/react/guides/mutations#persist-mutations)

## Query Invalidation

*Waiting for queries to become stale* before they are fetched again doesn't always work, especially when you *know for a fact that a query's data is out of date* because of something the user has done. For that purpose, the **`QueryClient`** has an **`invalidateQueries`** method that lets you intelligently mark queries as stale and potentially refetch them too!

When a query is invalidated with **`invalidateQueries`**, two things happen:

- It is marked as stale. This stale state overrides any **`staleTime`** configurations being used in **`useQuery`** or related hooks
- If the query is currently being rendered via **`useQuery`** or related hooks, it will also be refetched in the background

### Query Matching with `invalidateQueries`

```jsx
import { useQuery, useQueryClient } from 'react-query'

// Get QueryClient from the context
const queryClient = useQueryClient()

queryClient.invalidateQueries('todos')

// Both queries below will be invalidated
const todoListQuery = useQuery('todos', fetchTodoList)
const todoListQuery = useQuery(['todos', { page: 1 }], fetchTodoList)
```

- Invalidate specific variables
    
    ```jsx
    queryClient.invalidateQueries(['todos', { type: 'done' }])
    
    // The query below will be invalidated
    const todoListQuery = useQuery(['todos', { type: 'done' }], fetchTodoList)
    
    // However, the following query below will NOT be invalidated
    const todoListQuery = useQuery('todos', fetchTodoList)
    ```
    
- Invalidate exactly
    
    ```jsx
    queryClient.invalidateQueries('todos', { exact: true })
    
    // The query below will be invalidated
    const todoListQuery = useQuery(['todos'], fetchTodoList)
    
    // However, the following query below will NOT be invalidated
    const todoListQuery = useQuery(['todos', { type: 'done' }], fetchTodoList)
    ```
    
- Even more granularity
    
    This function will receive each **`Query`** instance from the query cache and allow you to return **`true`** or **`false`** for whether you want to invalidate that query
    
    ```jsx
    queryClient.invalidateQueries({
      predicate: query =>
        query.queryKey[0] === 'todos' && query.queryKey[1]?.version >= 10,
    })
    
    // The query below will be invalidated
    const todoListQuery = useQuery(['todos', { version: 20 }], fetchTodoList)
    
    // The query below will be invalidated
    const todoListQuery = useQuery(['todos', { version: 10 }], fetchTodoList)
    
    // However, the following query below will NOT be invalidated
    const todoListQuery = useQuery(['todos', { version: 5 }], fetchTodoList)
    ```
    

### Invalidation from Mutations

When a mutation in your app succeeds, it's VERY likely that there are related queries in your application that need to be invalidated and possibly refetched to account for the new changes from your mutation.

```jsx
import { useMutation, useQueryClient } from 'react-query'

const queryClient = useQueryClient()

// When this mutation succeeds, invalidate any queries with the `todos` or `reminders` query key
const mutation = useMutation(addTodo, {
  onSuccess: () => {
    queryClient.invalidateQueries('todos')
    queryClient.invalidateQueries('reminders')
  },
})
```