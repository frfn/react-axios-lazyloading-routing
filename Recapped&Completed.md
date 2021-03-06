# AsyncComponent, Axios, Routing, Lazy Loading-Rrecapped and Completed

<br>

# Categorized

Takeaways:

-   Lazy Loading:

    -   `asyncComponent()`
    -   `lazy()` and `<Suspense>`

-   Axios

    -   axios instance
    -   interceptors
    -   `post()` | `get()` | `put()` | `delete()`

-   `React.Fragment()`

-   Routing
    -   NavLink
    -   Link
    -   Switch
    -   BrowserRouter
    -   Redirect
    -   Route
    -   Dynamic Routing

<br>
<br>

# Notes

-   Created a GitHub so I can push changes and store them
-   Works as expected, first glance, 4 main files with Blog.js being the main file where all the components will go
-   NewPost.js is stateful while all our stateless (changed)
-   They are all class based components since we will be using lifecycle methods, we can use React Hooks here as well
-   Lazy Loading is used in Burger Builder, **NOT** here!! Pretty easy to implement, used for optimization!

<br>
<br>

# 1. Starting the AJAX / HTTP requests

-   We can use the built in `XML` / `HTTP` request methods but that will be cumbersome, we will use a third party library called `Axios`:

    -   `Axios`

        -   I can add to any React Application, it is JavaScript and used for XMLHTTPRequests
        -   `npm install axios --save`
        -   `import axios from '../locOfAxios'`

    -   `Axios` is `Promise` based

        -   it will have something to report back to you
        -   3 states
            -   `pending`
            -   `fulfilled`
            -   `rejected`
        -   This means that the whole web page can load and does not need to wait for the process to finish, `Axios` is ASYNC + `Promise` based
        -   `Synchronous` VS `Asynchronous`:
            -   Sync is **_one_** process at a given time
            -   Aysnc is **_multiple_** processes at a given time

    -   `axios.get()` is async, it does not finish immediately, it needs time to go to the server and collect data

-   Manipulate data!

    -   Since response.data is an array, we can use methods on it and shorten it, map it, reduce, etc!

    -   In `Blog.js,` we have shortened it (using `splice()` method) and added an author property with the help of the spread operator ( ...post ) and `.map()`

    -   Working with async methods should be thought of ahead of time, here I faced a problem where I am getting an error from `FullPost.js`
        -   Network Loop, because of LifeCyclye component

<br>
<br>

# 2. Getting familiar with data

-   `axios.get('url').then( ..code ..).catch( ... )`

    -   this will return a JSON formatted data from the URL, in the example, the server we're pinging is `RESTful`. So it returns a JSON formatted data

-   `axios.post('url', {obj})`
    -   we are sending an object to the server, and `POSTing` it

<br>
<br>

# 3. NewPost.js

-   I got ahead of myself and created something that would be nice if there were multiple forms. Using `dynamic object naming notation`, in setState, setting the values

-   I am getting over my head tbh, stay focused, and don't worry about 'remembering' all the things. No one knows everything. **_Stay motivated!_** Okay? :)

-   `axios`

    -   I am using `axios.post(url, obj, config)` which takes in three arguments!
    -   look at `NewPost.js `to see how it works

EXTRA:

-   added a 'Loading...' in the button component - was wondering how I can have text while the POST process happening, USE `REDUX`. EDIT!

<br>
<br>

# 4. deletePostHandler method

-   `axios.delete(URL)`

-   I took a look at how `.delete()` works, it is the URL that you need to delete the item

-   it is `async` / `promise` based SO it will return a response object

<br>
<br>

# 5. Blog.js

-   `.catch()` has been implemented and it is to catch if there are errors that occurs

-   created a property in state, `error: false`

-   set error to true in `.catch()` so that it indicates that there is an error that occured

-   changed the String for 'posts' so that it can display 'Oops, something went wrong...'

-   Done with an if statement, if ( !this.state.error ) { ..show posts.. }

<br>
<br>

# 6. Interceptors – so we look at the requests and responses

-   I go to the most global file, `index.js`

-   `index.js` is what is mounted to the DOM

-   `import axios from 'axios'`

-   if I intercept, it will BLOCK the current request for `Blog.js`

    -   to fix, return the requestConfig object!

-   The idea behind interceptors is that I can edit request configs

    -   I can add headers, stuff like that
    -   Powerful because we can add authorization headers as well

-   the second argument is for errors

-   you can add or remove by

    `axios.interceptors.request/response.use/eject(requestConfig/responseConfig => { .. code ..})`

<br>
<br>

# 7. Setting default settings

-   Ease of use: instead of writing the URL every time, I can configure a setting

    -   `axios.defaults.baseURL = 'url'`

-   Accessing headers and adding/modifying/deleting values in the property

<br>
<br>

# 8. Creating and Using Axios Instances

-   created a new file, `axios.js`

-   This is a copy of the axios object

-   commented out axios baseURL and common['Auth'] and put it in axios.js

    -   Creating a new instance!

-   export default instance; -- its like exporting class or functional components

-   don't forget to change all of the classes that use Axios to use the newly created instance!

-   Note: I do not see the interceptors console log anymore (the request and response) because the setter was set up for the GLOBAL axios object

<br>
<br>

# 9. ROUTING

1.  Enables SPA properties
    -   Multiple pages in a single page
    -   One server, multiple pages, it is done by routing
2.  Prep
    -   `Blog.js`
        -   created a header --> nav --> ul --> li, a href="/" | href="/new-posts"
        -   created a CSS for the ul, li, a tags
3.  Setting Up
    -   n`pm install --save react-router react-router-dom`
        -   MUST have both dependencies react-router AND react-router-dom
        -   `--save` so it SAVES in the package.json
    -   router is NOT by Facebook
4.  Start
    -   comment out FullPost and NewPost
    -   `"/"` is root path
    -   `"/new-post"` is new post path, etc.
    -   In Index or App, you MUST wrap part of the app that should render routes
        -   Did in `App.js`
        -   ` <BrowserRouter>` enables routing!
            -   Wraps <Blog /> so any component in Blog will get the logic for Routing
    -   Created new folder in Blog folder, Posts
    -   Moved NewPost and FullPost inside container/Blog because these are now DISTINCT pages because of routing
5.  `React Router` vs `React Router Dom`
    -   historically React Router is what you'd need, but React Router Dom is ultimately the dependency you need
6.  Moved all the Post logic, state and code into Posts.js
    -   Moved entirety of code from Blog.js to Posts.js, including the componentDidMount
    -   removed the selectedPostId and error property in the state!
        -   not needed because it was used in the Blog.js
7.  Blog.js is just a skeleton now, a framework for the components to be in
    -   Reformatted the Blog.js, modularized is all I did
8.  Routing

    -   Using the `<Route />` tag to route to different 'pages' - also gives props to the component

        -   RESERVED WORDS TO REMEMBER:

            -   exact (for '/') - boolean value, by using this it will create an quasi-absolute path, if I do post/2, it will not load!
            -   path="url_loc"
            -   render={() => {jsx}} - Anonymous Function
            -   component={component-name}, not the TAG (<Posts />) just 'Posts'

            \*\* use component keyword as a default. Only use render for small messages.

        `<Route path='/' exact render={() => {jsx}}/>`
        `<Route path='/' exact component={Posts}`

9.  Reloading Issue?

    -   We do not want to Reload because state will be refreshed and state will go away and restart.
    -   How to stop that:

        -   DO NOT use <a href>, use `<Link>` from `'react-router-dom'` if using routing.
        -   `<Link />` reserved words
        -   `to='/'` - also accepts objects

        ```
        to={{
                pathname: 'loc',
                hash: '#submit',  -- the fragment
                search: '?submit=true'  -- the query
            }}
        ```

10. Using 'component' inside the `<Route component={Posts} />` is more recommended because more info is given

-   In action: render VS component, render reserved word does NOT give this.props information, no object is given!

-   IN URL: - new-post/2? ...

-   isExact in this.props changes to false as it is not EXACT path

    10a. Had to recap how the Post.js and Posts.js works - Collecting the post.id from .map() in Posts.js - method grabs the id when the `<div> `.. `<article>` has been clicked on - IT WILL have its own data since the `.map()` iterates through all the items

11. import { withRouter } from 'react-router-dom'

-   adds router information to a component

-   used on Post.js to give more information for routes, it will give the props!

-   a HOC wrapper: `export default withRouter(post)`

-   it will make the component 'Route Aware', it will GIVE access to router settings to the component!

12. `Absolute Path` VS `Relative Path`

-   Absolute:

    -   always appended to root domain

    -   example.com/new-post <-- main URL

    -   example.com/post/new-post <-- the URL will omit /post/

    and convert to: example.com/new-post

-   Relative:

    -   this.props.match.url + '/new-post'

    -   it appends the '/new-post' at the end of the previous URL

    -   it becomes a relative path!

    -   There is NO better way, pick any.

    12a. Absolute vs Relative Paths (Article)
    You learned about `<Link>` , you learned about the to property it uses.
    The path you can use in to can be either absolute or relative. - Absolute Paths
    By default, if you just enter to="/some-path" or to="some-path" , that's an absolute path.
    Absolute path means that it's always appended right after your domain. Therefore, both syntaxes (with and without leading slash) lead to example.com/some-path . - Relative Paths
    Sometimes, you might want to create a relative path instead. This is especially useful, if your component is already loaded given a specific path (e.g. posts ) and you then want to append something to that existing path (so that you, for example, get /posts/new ).
    If you're on a component loaded via /posts , to="new" would lead to example.com/new , NOT example.com/posts/new .
    To change this behavior, you have to find out which path you're on and add the new fragment to that existing path. You can do that with the url property of props.match :

    `<Link to={props.match.url + '/new'}>`

    will lead to example.com/posts/new when placing this link in a component loaded on /posts . If you'd use the same <Link> in a component loaded via /all-posts , the link would point to /all-posts/new .

    There's no better or worse way of creating Link paths - choose the one you need. Sometimes, you want to ensure that you always load the same path, no matter on which path you already are => Use absolute paths in this scenario.
    Use relative paths if you want to navigate relative to your existing path.

13. Link VS NavLink component

    -   activeClassName='active-Name'

        -   instead of class="active", you can change the class name to however you like!

    -   activeStyle={{
            color: 'blue',
            textDecoration: 'underline'
        }}

        -   this gives the NavLink inline styling!

    -   similar to Link but adds extra props to give styling to the link!
        from: import { Route, Link } from "react-router-dom";
        to: import { Route, NavLink } from "react-router-dom";

        -   We now have an '.active' class we can use!
        -   In the CSS, adding Blog a.active will change the color
            -   BUG: Both Links are highlighted... why? The '/' is treated as prefixes, since both '/' and '/new-posts' has '/', it treats both!
            -   FIX: add 'exact' in the Link tag, it tells the Router, NO, it's not a prefix, it's the full path!

14. Clicking on Posts
    -   we can render <Route path='...' exact component={comp} /> to the new components
        BUT
    -   we need `dynamic routing parameter`!
        -   '`/:id`' is dynamic and is used as `this.props.match.params.id` -- it is passed from `<Route>` tag, `<Route>` gives more routing props!
        -   id can be anything, '/:num', it will be ...params.num
        -   `<Route path='/:id'` ... the `:id` is **DYNAMIC**. This is how you implement it in REACT ROUTER
        -   add after `'/new-post'` because after `'/:' `the router can accidently think new-post is an ID

IMPORTANT for changing pages, dynamically changing variable names!

-   `<Route path='posts/:id' exact component={FullPost} />`

-   `<Link key={post.id} to={'posts/' + post.id }><div></div></Link>`

        - THIS IS HOW YOU CHANGE PAGES DYNAMICALLY!. + More EFFICIENTLY IN JSX

15. FullPost - changed from componentDidUpdate to componentDidMount

    -   `params.id` is coming from the dynamic path -- in `<Route path='/:id' />`
        -   `params: { id: '1' }`
        -   match, params, history all has to do with the` <Route />` tag!
    -   console logging, we see that params NOW includes an `'id'`
    -   'id' comes from the dynamically changing `':/id'`
    -   if `( this.props.match.params.id )` from if `( this.props.id )`
    -   `axios.get('posts/' + this.props.match.params.id).then(resObject => {this.setState({})})`

16. NewPost

    -   new `URLSearchParams`

        -   grabs the key value pair of a QUERY.
        -   But how do you extract search (also referred to as "query")
            parameters (=> ?something=somevalue at the end of the URL)?
            How do you extract the fragment (=> #something at the end of the URL)?

            <Link to="/my-path?start=5">Go to Start</Link>

        or

        ```
        <Link
            to={‌{
                pathname: '/my-path',
                search: '?start=5'
            }}
            >Go to Start
        </Link>
        ```

        You probably want to get the key-value pair, without the ? and the = - do not forget the 'new' reserved word, creates new instance

        ```
        const query = new URLSearchParams(this.props.location.search)
        for(let params of query.entries()) {
            console.log(params)
        }
        ```

    -   Fragment

        -   <Link to="/my-path#start-position">Go to Start</Link>

            or

            <Link 
                to={‌{
                    pathname: '/my-path',
                    hash: 'start-position'
                }}
                >Go to Start
            </Link>

    -   React router makes it easy to extract the fragment.
        You can simply access the Fragment by traversing to (props.location.hash)

17. Without the 'posts' in '/posts/:id' in Blog.js + <Link to='/posts/ ..'>, both the FullPost and NewPost component would render

    -   Flex Fix: add the /posts/
    -   More robust way:
        -   `import { Switch } from 'react-router-dom';`
        -   Switch only loads one route!
            -   Just know that if you use switch, order of the routes is important.
                -   Else it will fail.
                    -   Ex. /:id and /new-post, new-post is NOT a valid id and would output an error.
                    -   In Blog.js the order is correct but if you put /:num above new-posts, it will be an error because new post is NOT a post in the JSON endpoint
    -   You can have this too, very flexible.
        <Route />
        <Switch>
        <Route />
        <Route />
        </Switch>
        <Route />

18. Navigating Programmatically

    -   In Posts.js, instead of <Link> linking to the routes when the posts are clicked, here is an alternative:
    -   Navigation is just a stack of pages, that's how we can go back and forward!
    -   this.props.history.push({pathname: '/' + id})
        ...push('/' + id)

    -   Using props.history.push() to navigate through the pages!
        -   Taking advantage of the history object
        -   push a new page on top of the 'stack' of pages!
        -   .push() and all the other props in history are methods!

19. Edge Case
    -   Home --> Posts, when clicking on a post it renders the 'Home' link to not be styled, changed the <Route> and <Link> in Blog.js
        and push() method in Posts.js
        to="/posts/'
        path="/posts/'
        .push({
        pathname: '/posts/' + id
        })
    -   You can face potential issues when using '/' to style
    -   'exact' reserved word is modified if you face this, the '/' path can cause issues if you want to style other components.
        So use more specific path names!
20. Nested Routes

    -   Currently, all routes are in Blog.js which are simply components that will be shown at the URL
    -   Moving FullPost <Route> to Posts.js!
        -   imported needed component, FullPost + Route
    -   We can use the <Route> tag in ANY component!

        -   Parent Component MUST be wrapped with <BrowserRouter>

    -   By moving the <Route> tag inside the Posts.js component, we now created a NESTED ROUTE.

        -   be careful that the URL reaches correctly, reaching ':/id' in Posts.js will not be possible BECAUSE of the '/' exact path in Blog.js
        -   by having the exact with '/', it will only FIND the '/' path and will stop there. Reaching any URL after gives nothing!
        -   changing the path of Route to {this.props.match.url} <-- that aims to the parent URL
        -   FullPost.js + Posts.js HAS 'num' params, I used 'id' and caused a bug, FullPost was not rendering.
        -   Important to know how to do NESTED ROUTES.

    -   BUG: When clicking on Post, the component is NOT rerendering.

        -   implement componentDidUpdate() in FullPost.js, also created loadData() method
        -   got infinite network loop because the if statement to check if id's (num) are not the same was not implemented correctly!
            instead of this.props.id --> this.props.match.params.num
            -   add a '+' to make variable into a number!
            -   new props ARE being passed, so componentDidUpdate must be implemented to loadData()!

    -   IMPORTANT FIX. componentDidUpdate + componentDidMount were used!

21. Redirecting to different URL

    -   you can render the same component with a different path!
        or
    -   <Redirect />
            <Redirect from='/' to='/posts/'
                if user goes to /, it will redirect to /posts!

    -   <Redirect /> in NewPost.js

        -   outside of <Switch> statement, you MUST use the 'to' property! We can not use 'from'
        -   Conditional Redirect, use state! Look at NewPost.js for example

    -   ANOTHER way, history prop! this.props.history!
        -   we already did it, this.props.history.push('/posts');

    Redirect VS push() - push() pushes next page on pages stack, you can also do replace() if you want the same behavior as Redirect - redirect replaces the current component and does not push to stack!

22. Navigation Gaurds - Crucial To Understand because this will serve for security purposes.

    -   Authenticated or not?
        Checks to see if user is AUTHENTICATED. There may be areas where the user MUST be authenticated to see the page, if not, don't render.
        -   In Blog.js:
            Added state and auth prop, used conditional rendering for this.state.auth
            Pretty cool, because <Redirect /> changes the URL location and component rendering to '/posts', since '/new-post' is null
        -   Alternative:
            Go to component that needs to be 'gaurded'
            -   In componentDidMount, check to see if user is authenticated!

23. 404 Case - if URL is unknown

    -   Using <Redirect /> handles 404 cases, if unknown URL is encountered, it redirects to a /posts, or you can create a 404 component and render here.

    Different Way:
    Use <Route render={() => {<h1>404 URL NOT FOUND</h1>}}/> - No path keyword is set! - Catches ALL route, even '/'

    -   Use either Redirect or Route to handle 404 cases, they will not work together!
        Since Redirect has 'from' it catches ALL routes that has '/'
        from='/' is treated as every URL
        -   How does it know?
            There's some magic happening in the back. If the URLb path is not specified by user, it will not be loaded. Pretty sick.

24. Loading routes LAZILY -- Good for efficiency, only load component when needed. Great if app has a LARGE file area that does NOT get visited regularly.

    -   The case of, if a user never visits a certain part of the SPA
    -   Only loads the one pages the user will go to, not ALL at once.
    -   Good for optimization
    -   Good to know because if we are downloading LARGE files, loading up the application will take longer than needed
    -   FIX:
        Code Splitting aka Lazy Loading
    -   How?:
        Needed React Router 4, and config from create-react-app

        -   Create a HOC wrapper
        -   Check asyncComponent.js in HOC folder

    -   Blog.js implements lazy loading
        when we import stuff, webpack (the build tool used behind the scenes) is informed about the dependency and include it in the bundle.js \*/
        code splitting, lazy loading, we don't want that. We only want that component to be loaded when needed.

        -   created new variable and executed asyncComponent.
        -   argument inside will be an Anonymous Arrow Function that returns an import() that leads to the NewPost.js
        -   In <Route ... component={asyncComponent}
            In network settings in Chrome, 2.chunk.js is now loaded -- this is an extra bundle that webpack created from the lazy loading that we just created.
        -   It didn't add the code to the main bundle, instead it prepared it when needed!! Awesome.

        -   This is how you load components asynchronously
        -   Useful for bigger apps!

24a. React Suspense -- Same as Lazy Loading -- IN "Downloads/66. React Suspense Start"
MUST NEED: React v16.6 - New method called the lazy() - official way to load components lazily! - Useful when Routing :) - No loading redundant code in advance - Great advantage because we do not have to use Routers for it if we do not need it

        React.lazy()
        <Suspense fallback={<div>...</div>}> <Posts /> </Suspense>

        Lazy loading is MUCH more important if files are large.

24b. Routing & The Server (Deployment)
User --> Server -->? React App - The server handles the requests first
--> issue is React knows the routes... not the server.
--> if we visit /post... there is no /post in our server, so it's a 404 error. It never reached the React App

            development server is configured differently (to load correctly), now we have to configure the server side too.
            --> MUST load and return index.html, especially in 404 cases! React will take over.
            --> if we have example.com/my-app, we MUST set base path! and not '/'
            --> CHECK App.js, basename='/' has been added to the BrowserRouter component!
                --> http://localhost:3000/my-app/posts it will now look like this
                --> if you are serving on the server side, you must configure the BASE name!

25. Assignment
    In file 66. ROUTER ASSIGNMENT, there are comments on there that are helpful for Routing needs.
