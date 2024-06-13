## DJS08 Project Brief: React Router
## 🎥 INSERT LOOM PRESENTATION LINK:
(https://www.loom.com/share/b2879778fca44495afaeefb4c4c1ccc6?sid=193663be-997f-4e5b-8be9-fbd46db7b4c7)

Are you ready to get stuck into some React Router? For this challenge, you are required to code along with the lecturer from this lesson on Scrimba V1 VanLife Project Bootstrapping or on Scrimba V2 click the link here VanLife Project Bootstrapping

The starter code has all the CSS styling required for the project; you will just need to link the corresponding classes as you code along. Jump into the start code here: GitHub Repository.

The focus for this project will be to understand routing and present your code. Along with your code, you will need to submit a recorded presentation talking through the presentation points included below.

React Routing Presentation Talking Points
For your recorded presentation, you will be discussing key concepts related to React Router, an essential tool for building single-page applications. To illustrate your understanding, address the following three questions in your presentation. These questions are designed to test your knowledge of the content from the "Advanced React Routing" Van Life Project, including setup, functionality, and application of React Router.

# Getting Started with installing the project
Install the dependencies and run the project and also install the chosen database firebase.
npm install firebase(installing the data)
npm install(Install the dependencies)
npm start

## Question 1: Explain the Setup and Basic Configuration of React Router
Purpose of React Router:
React Router is used to manage navigation and routing in a React application, allowing developers to create single-page 
applications with multiple views.In order to set it up one needs to run npm install react router on the command line.

Setting up React Router:
To set up React Router, you need to wrap your application with the BrowserRouter component along with installing router on the command line, which enables routing functionality using the browser's history API.In this Van Life Project we see this  being implemented in index.jsx where the App() is rendered using 
 ReactDom.render() API.


Role of <Routes> and <Route>:

<Routes>: This component is a container for all the route definitions in your application.It is always the child of BrowserRoutes as seen in index.jsx some developers utilize aliasing and import Browserrouter as Router.
<Route>:<Route> has a path and element prop which allows the desired component to be rendered. Each <Route> defines an URL  path and the component that should be rendered when the application navigates to that path.




Question 2: Application of Route Parameters and Nested Routes
Route Parameters:
Route parameters are dynamic segments in the URL that can be accessed within the route component. The useParams() hook is used to retrieve these parameters in the component.In this project we see these being implemented to diplay the Van information for each van as indicated by the code  snippet  <Route path="vans/:id" element={<HostVanDetail />}> clicking on each van shows us the details of that specific van allowing for reusability. 


Nested Routes:
Nested routes allow you to define routes within other routes,creating a nested structure. This helps in organizing the application  and managing complex UI structures by breaking them into smaller, reusable components.Having Nested routes also allows us to utilize the <Outlet> component we can see that we have nested roots when defining our App component.
   
```javascript    
    <Route element={<AuthRequired />}>
            <Route path="host" element={<HostLayout />}>
              <Route index element={<Dashboard />} />
              <Route path="income" element={<Income />} />
              <Route path="reviews" element={<Reviews />} />
              <Route path="vans" element={<HostVans />} />
              <Route path="vans/:id" element={<HostVanDetail />}>
                <Route index element={<HostVanInfo />} />
                <Route path="pricing" element={<HostVanPricing />} />
                <Route path="photos" element={<HostVanPhotos />} />
              </Route>
            </Route>
          </Route>
```


          
In this code snippet we have nested routes and route parameters.These nested routes allow us to use <Outlet> component we can see in this code snippet.Using outlet allows us to pass context through it and using the useOutletContext hook which is used to pass data between our components using the useOutletContext hook.

```javascript
export default function Layout() {
    return (
        <div className="site-wrapper">
            <Header />
            <main>
                <Outlet />
            </main>
            <Footer />
        </div>
    )
}
```


Question 3: Implementation of Navigation Controls and Dynamic Linking
<Link> Component:
The <Link> component is used for navigation, allowing users to move between different routes without a full page reload, maintaining a smooth single-page application experience.

NavLink for Active Styling:
NavLink is similar to Link but includes additional functionality for active styling, allowing developers to apply specific styles to the active link, enhancing the user experience.

We can see both of these link being used in the following code snippet below.Navlink allows us to insert the activeStyles object as a prop styling the active link in the navigationbar.
 
 
```javascript 
 export default function Header() {
    const activeStyles = {
        fontWeight: "bold",
        textDecoration: "underline",
        color: "#161616"
    }

    function fakeLogOut() {
        localStorage.removeItem("loggedin")
    }

    return (
        <header>
            <Link className="site-logo" to="/">#VanLife</Link>
            <nav>
                <NavLink
                    to="/host"
                    style={({ isActive }) => isActive ? activeStyles : null}
                >
                    Host
                </NavLink>
```



Search Parameters and useSearchParams Hook:
Search parameters are used to filter and sort content dynamically. 
The useSearchParams hook provides an API to read and manipulate the query string of the URL, enabling features like filtering van listings based on user input in the VanLife project.In this projects we see this hook being used to filter the van projects in the Vans.jsx file.We can see this hook being implemented in the following code snippets.

  ```javascript
  const [searchParams, setSearchParams] = useSearchParams()
   // useSearchParams hook is used to read and manipulate the query parameters in the URL. 
    // It returns an array with the current search params and a function to update them.
```

```javascript 
 const typeFilter = searchParams.get("type")
    // Retrieve the "type" parameter from the URL query parameters.
```
    
    
We can see the filtering being implemented in the code snippets since we have buttons which will filter the type of van in this project.
```javascript
     <div className="van-list-filter-buttons">
                <button
                    onClick={() => handleFilterChange("type", "simple")}
                    className={
                        `van-type simple 
                        ${typeFilter === "simple" ? "selected" : ""}`
                    }
                >Simple</button>
                // Button to filter vans by type "simple". 
                // Applies the "selected" class if the typeFilter matches.
```

Using the handlefilterchange function and the UseSearchParams hook we can filter the van types.
The handlefilterChange function uses the UseSearch hook to filter the vans using an if statement.

   ```javascript
function handleFilterChange(key, value) {
    // Function to handle filter changes.

        setSearchParams(prevParams => {
            if (value === null) {
                prevParams.delete(key)
                // If the value is null, delete the corresponding search parameter.
            } else {
                prevParams.set(key, value)
                // Otherwise, set the search parameter to the new value.
            }
            return prevParams
            // Return the updated search parameters.
        })
    }
```  


