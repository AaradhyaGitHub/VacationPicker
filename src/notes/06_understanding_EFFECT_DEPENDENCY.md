What are Effect Dependencies? 

Effect Dependencies are prop or state values that are used inside of the effect function. 

In addition, other effect dependencies would be functions or context values that depend on or use state or porps. 

Any value that causes component to execute again basically state and props any such value is a dependency if used inside a useEffect function 

Other values like Refs, browser built in objects or methods are NOT Effect Dependencies 

useEffect only cares about dependencies that would cause the component function to execute again...

WHY this matters? 
--> Because our effect function should run whenever the component function executes if one of it's dependencies changed

With an empty array, they can't change. So in App component's useEffect only executed once 

But in Modal, we are using the open prop...
now it's different. 
So, we have to add open to our dependency array.