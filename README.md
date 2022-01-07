# Numerical Basics Project
### About: 

For this project, I implemented an application using Shiny-R. I used shiny to build the project. I created a simple code to multiply and add two different variables the user chooses from a slider thats on the application.

### Results:

First, I  created the UI (User Interface) for the shiny application with a *fluidPage* layout.

```R
library(shiny)
ui <- fluidPage(
  sliderInput("x", "If x is", min = 1, max = 50, value = 30),
  sliderInput("y", "and y is", min = 1, max = 50, value = 5),
  "then, (x * y) is", textOutput("product"),
  "and, (x * y) + 5 is", textOutput("product_plus5"),
  "and (x * y) + 10 is", textOutput("product_plus10")
)
```

The UI is similar to the ingredients in a recipe. So lets list out the ingredients and what they do.

*sliderInput* constructs a slider widget to let the user select a numeric value from a range.

*textOutput* displays the code and will later help me print the data.

Now lets focus on the server. The server is the directions in the recipe. The ingredients will be used as the directions describes them.

```R
server <- function(input, output, session) {
  
  # create a reactive expression
  
  product <- reactive({
    input$x * input$y
  })
  
  output$product <- renderText({ 
    
    product()
  })
  output$product_plus5 <- renderText({ 
    
    product() + 5
  })
  output$product_plus10 <- renderText({ 
  
    product() + 10
  })
}
shinyApp(ui, server)
```

So lets list out the directions and what they do.

First, I created a reactive. Reactive expressions let me control which parts of my app update when, which prevents unnecessary computation that can slow down my app. In this case, it optimizes the code by having less code written which increases the apps speed.

*output$product*/*output$product_plus5*/*output$product_plus10* variables are set to *renderText* which is paired with *textOutput*. This is because the server side of the code uses a specific render function to wrap the code that is provided.

In this case, the *renderText* prints a summary of the dataset.

Each render{Type} function is designed to produce a particular type of output (e.g. text, tables, and plots), and is often paired with a {type}Output function.

Finally, I write down the code shinyApp(ui, server) which constructs and starts the Shiny application from UI and server.

**Final Product:**

![Screen Shot 2021-11-02 at 3 21 19 PM](https://user-images.githubusercontent.com/89553126/139946342-cee4eb71-954d-4f81-b473-92253492cdad.png)
