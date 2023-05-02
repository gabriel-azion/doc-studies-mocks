# Edge Functions ChatGPT integration

Chat GPT can be used in almost all tasks that involves understanding or generation of natural language or code. In the development environment, it can be a tool for boosting developers productivity, being able to:

- Explain the code being implemented.
- Generate new code.
- Refactor preexisting code.

---

## How does the Edge Functions ChatGPT integration work?

First, it's necessary to configure your credentials registered on the OpenAI platform.

With your credentials in hand, paste them in your function args.(CONFIRMAR ISSO)

```json
exemplo de config das credentials do gpt
```

Now, with your credentials set, you're able to use the integration to develop faster and have your code reviewed whenever you like.

---

## Features

### Code Explanation

One feature available on this integration is the Code Explanation. It comes in handy when you have to debug a function, or simply review it. It's quite useful when you're working on legacy code.

### Code Generation

Code Generation works based on the prompt informed. For example, let's say you want to return a `HTML` page, with a table containing the name, phone number and address.

**Prompt**: 
```
    // generate a html table with name, phone number and address
```

After writing the prompt inside the code editor, right click it and select `ChatGPT: Generate`

**Output**:
```html
    <body>
     <table>
       <thead>
         <tr>
           <th>Name</th>
           <th>Phone Number</th>
           <th>Address</th>
         </tr>
       </thead>
       <tbody>
         <tr>
           <td>John Smith</td>
           <td>(123) 456-7890</td>
           <td>123 Main St, Anytown, USA</td>
         </tr>
         <tr>
           <td>Jane Doe</td>
           <td>(987) 654-3210</td>
           <td>456 Oak St, Anytown, USA</td>
         </tr>
         <tr>
           <td>Bob Johnson</td>
           <td>(555) 555-1212</td>
           <td>789 Maple St, Anytown, USA</td>
         </tr>
       </tbody>
     </table>
    </body>
```

### Code Refactor 

Another option is to ask ChatGPT to refactor the code. To do so, you have to select the piece of code you want to have refactored, then right click on it and select `ChatGPT: Refactor`. After that, your code will be refactored automatically. 

Note that it's always a good idea to test and ensure the refactored code is working as expected, avoiding unexpected issues in the future.

---

## Implementation

Here are some real-life implementations of the Preview Deployment tool:

| Implementation | Description   |
|---|---|
|  How to preview a function that returns a HTML page | xxxxx |
|  How to return data in JSON with ChatGPT and Azion Preview Deployment | xxxxx |


## See also

- [x]()
- [x]()
- [x]()
- [x]()