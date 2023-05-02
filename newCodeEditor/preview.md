# Code Preview (Preview Deployment)

Azion Preview Deployment makes it possible for you to preview the behavior of your edge functions before they go to production. New possibilities are unlocked when using the Preview, such as:

- Test different flows based on the http method provided.
- See the outcome of an HTML page.
- Return data in JSON.

---

## How does Preview Deployment work?

Azion Preview Deployment works with the aid of an auxiliar function inside your source code. This function is called `PreviewProvider`, and it makes it possible to simulate a request. This `PreviewProvider` function is represented as:

```javascript
    function PreviewProvider<PreviewProvider>(args){
        var request ={
            body:{},
            headers{},
            method: "GET",
            redirect: ""
        }
        return handleRequest(request)
    }
```

Now, with your simulated request running, you're able to set different behaviors to your function, based on all properties available inside the request variable, such as:

```javascript
    async function handleRequest(request){
        switch (request.Method){
            case: 'GET':
             return new Response(html,{
                headers:{
                    "content-type":"text/html:charset=UTF-8",
                }
             })
        }
    }
```

In this code snippet, it's defined that if a `GET` request is called, it returns the `HTML` var, containing the html to be output, and set its content type as required to perform this action.

## Preview Provider and ChatGPT

The ChatGPT integration helps you to boost your productivity and, alongside the Preview Deployment, enable more analytic implementations, making it possible to test and see new ideas on the fly. Take a look at [How to use ChatGPT to boost your productivity coding at the edge]().

## Implementation

Here are some implementations of the Preview Deployment tool:

| Implementation | Description   |
|---|---|
|  How to preview a function that returns a HTML page | xxxxx |
|  How to return data in JSON with ChatGPT and Azion Preview Deployment | xxxxx |


## See also

- [x]()
- [x]()
- [x]()
- [x]()