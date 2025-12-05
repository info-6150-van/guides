## Code review guidelines

### Introduction

Reviewing code is an essential skill for frontend engineers, and other software professional, to develop. However, it is quite often overlooked and not taught correctly. This guide will give you some general guidelines into how to approach it practically. It is, however, not a one size fits all solution, teams and engineers might evolve and the tips in these documents might become outdated or might not be applicable in your specific scenario, however, the general process and strategies are less likely to change, so focus on learning and practicing those.

### The Review Process

It is common for most unexperienced engineers to tackle a code review as a simple as "reading" the code. Although this is the action you will be taken in order to understand the information you were giving, it is not the correct mindset when approaching this process. Due to the amount of information and layers or understanding that you need to overcome. Think about it for one second, the first time you read a book, you will not understand all its nuances, you might get the overall story arc, the characters and the roles they play, but more detailed and critical information might require more than one read to fully grasp, such as: historical context, personality traces, cultural gestures and relationships, etc. 

The same logics applied for code reviews, don't expect to identify all "issues" and improvements in a single read pass, instead focus into systematically search for specific improvements that you know it might be present. For that, I recommend curating a checklist, each item in this list represents a reading, start to finish, of the coding you will be reviewing. As you read the code, I strongly suggest you make notes to yourself, some of them might become comments for the reviewer. 

In order to distinguish between a self comment and a comment to the reviewer, you will need to answer a simple question: "Will that improve the code?". That is a complex question to answer due to its ambiguous nature. There are attempts to help it reduce it, for example, establishing coding guidelines, such as style guides, naming convention, establishing libraries that need to be used, etc. For the exam, I will not consider style comments as valid, since those are usually opinionated, they were not discussed in class, and they don't allow me to evaluate your understanding of the class content. Instead, focus on the practical aspect of topics that were discussed in class. Such as: best practices, performance and actual problems with the code. 

### Example

I will walk you through an example reviewing the code below. This example will follow an approach I suggest you take during the exam. I will make comments and will mark those comments as `[REVIEWER]` and `[SELF]` to distinguish between comments that are for my own personal sake and comments that I think pass the bar of "Will that improve the code?". For example:

```js
// [REVIEWER] 'number' is a reserver key word in js.
// I suggest changing it to 'upperAccLimit'.
function doSomething(number) {
	// [REVIEWER] 'var' keyword causes hoisting which
	// can lead to unexpected behaviour, change to 'let'. 
	var acc = 0;
	
	// [SELF] Using ++x prevents some issues.
	for(let x = 0; x < number; x++){
		// [SELF] I prefer 'acc += x'.
		acc = acc + x;
	}
	return acc;
}
```

The code we will review is a User Profile, it is meant to showcase the user information, its main logic is about retrieving data from the server in react. I will provide multiple code reviews, each focusing in a single aspect of my code review checklist. Which contains the following topics:

```
- Is the code readable?
- Do I clearly understand what the code is doing? 
- Does it do what is supposed to?
- Does it follow best practices?
- Are there any security issues?
- Are there any performance concerns?
```

Here is the code we need to review: 

```js
export function UserProfile({ user }) {
    const [isLoading, setIsLoading] = useState(true);
    useEffect(() => {
        fetch(`/api/users/${user.id}`)
            .then(response => response.json())
            .then(data => {
                setUserDetails(data);
                setIsLoading(false);
            });
    }, [user]);
    if (isLoading) return <div>Loading...</div>;
    return (
        <div>
            {user.name}
            {user.email}
            {user.phone}
        </div>
    );
}
```

#### Pass 1: Is the code readable?

```js
// [SELF] The code is quite cluthered, I would add some empty spaces.
export function UserProfile({ user }) {
    const [isLoading, setIsLoading] = useState(true);
    useEffect(() => {
		    // [SELF] I prefer async/await
        fetch(`/api/users/${user.id}`)
            .then(response => response.json())
            .then(data => {
                setUserDetails(data);
                setIsLoading(false);
            });
    }, [user]);
    if (isLoading) return <div>Loading...</div>;
    return (
        <div>
            {user.name}
            {user.email}
            {user.phone}
        </div>
    );
}
```

#### Pass 2 : Do I clearly understand what the code is doing?

```js
// [SELF] The code is fetching the user data, but it doesn't 
// show it to the user, since it saved using a 'setUserDetails' function
// which, from the snippet, I cannot know where it is comming from.
// I will assume it sets the user variable.
export function UserProfile({ user }) {
    const [isLoading, setIsLoading] = useState(true);
    useEffect(() => {
        fetch(`/api/users/${user.id}`)
            .then(response => response.json())
            .then(data => {
		            // [REVIEWER] It is not clear where 'setUserDetails' is comming from.
		            // Is it a bug in the logic? Or can you add a comment giving the missing 
		            // context to understand it? 
                setUserDetails(data);
                setIsLoading(false);
            });
    }, [user]);
    if (isLoading) return <div>Loading...</div>;
    return (
        <div>
            {user.name}
            {user.email}
            {user.phone}
        </div>
    );
}
```

#### Pass 3 : Does it do what is supposed to?

Here I will report any bugs I've found.

```js
export function UserProfile({ user }) {
    const [isLoading, setIsLoading] = useState(true);
    useEffect(() => {
        fetch(`/api/users/${user.id}`)
            .then(response => response.json())
            .then(data => {
                setUserDetails(data);
                // [REVIEWER] This is a bug, if this request fails, we will never,
                // update `isLoading`, causing the user to be stuck in the loading stage forever. 
                setIsLoading(false);
            });
    // [REVIEWER] Assuming `setUserDetails` updates the user property in this component,
    // letting 'user' be a dependency here, might trigger an infinite update loop.
    // Because everytime we successfully complete the data fetch, 'user' will be updated,
    // trigering this effect again.
    }, [user]);
    if (isLoading) return <div>Loading...</div>;
    return (
        <div>
            {user.name}
            {user.email}
            {user.phone}
        </div>
    );
}
```

#### Pass 4 : Does it follow best practices?

```js
export function UserProfile({ user }) {
    const [isLoading, setIsLoading] = useState(true);
		
    useEffect(() => {
				// [REVIEWER] It is better to just use: ReactQuery to handle this.
        fetch(`/api/users/${user.id}`)
            .then(response => response.json())
            .then(data => {
                setUserDetails(data);
                setIsLoading(false);
            });
            // [REVIEWER] You are missing the error handling logic, those should
            // always be present in fetch requests.
    }, [user]);
    if (isLoading) return <div>Loading...</div>;
    return (
        <div>
            {user.name}
            {user.email}
            {user.phone}
        </div>
    );
}
```

#### Pass 5 : Are there any security issues?
```js
export function UserProfile({ user }) {
    const [isLoading, setIsLoading] = useState(true);
		
    useEffect(() => {
				// [REVIEWER] How are we handling authentication?
				// We shouldn't be able to fetch user data without
				// proper auth handling.
        fetch(`/api/users/${user.id}`)
            .then(response => response.json())
            .then(data => {
                setUserDetails(data);
                setIsLoading(false);
            });
    }, [user]);
    if (isLoading) return <div>Loading...</div>;
    return (
        <div>
            {user.name}
            {user.email}
            {user.phone}
        </div>
    );
}
```

#### Pass 6 : Are there any performance concerns?

```js
export function UserProfile({ user }) {
    const [isLoading, setIsLoading] = useState(true);
		
    useEffect(() => {
		    //[REVIEWER] What is our caching strategy here? 
		    // Also, how are we syncing those request? Out of order
		    // Server request might lead to undefined behaviour in our UI.
        fetch(`/api/users/${user.id}`)
            .then(response => response.json())
            .then(data => {
                setUserDetails(data);
                setIsLoading(false);
            });
    }, [user]);
    if (isLoading) return <div>Loading...</div>;
    return (
        <div>
            {user.name}
            {user.email}
            {user.phone}
        </div>
    );
}
```

#### Final Answer:

```js
export function UserProfile({ user }) {
    const [isLoading, setIsLoading] = useState(true);
		
    useEffect(() => {
        fetch(`/api/users/${user.id}`)
            .then(response => response.json())
            .then(data => {
                setUserDetails(data);
                setIsLoading(false);
            });
    }, [user]);
    if (isLoading) return <div>Loading...</div>;
    return (
        <div>
            {user.name}
            {user.email}
            {user.phone}
        </div>
    );
}
```

- What is our caching strategy here? Also, how are we syncing those requests? Out of order 
   server request might lead to undefined behaviour in our UI.
   
- How are we handling authentication? We shouldn't be able to fetch user data without
   proper auth handling.
   
- 	It is better to just use: `ReactQuery` to handle this.

-   You are missing the error handling logic, those should always be present in fetch requests.

-   Why not use the `Suspense` API from React to handle the loading fallback. 

- This is a bug, if this request fails, we will never, update `isLoading`, causing the user to
   be stuck in the loading stage  forever.
    
-   Assuming `setUserDetails` updates the user property in this component,
    letting 'user' be a dependency here might trigger an infinite update loop.
    because every time we successfully complete the data fetch, 'user' will be updated,
    triggering this effect again.

- It is not clear where `setUserDetails` is coming from.
  Is it a bug in the logic? Or can you add a comment giving the missing 
 context to understand it? 

### Comments about the review

Notice that I don't provide a clear answer to all questions. Some I just raised the problem, that is okay,
is NOT the reviewer responsability to provide solution to code issues. Focus into identifying and justifying
why it is worth taking a look. Also, The suspense comment I remembered while adding the final comments,
that is okay and it happens sometimes, since it might take a while for us to recall all details about the code.


