# Fullstack-Open-Part1
Exercise submissions for part 1

> # Exercises 1.1. - 1.2. (Solutions)
The exercises are submitted via GitHub, and by marking the exercises as done in the [submission application](https://studies.cs.helsinki.fi/stats/courses/fullstackopen).

https://fullstackopen.com/en/part1/introduction_to_react#exercises-1-1-1-2

The exercises are submitted **one part at a time**. When you have submitted the exercises for a part of the course you can no longer submit undone exercises for the same part.

Note that in this part, there are [more exercises](https://fullstackopen.com/en/part1/a_more_complex_state_debugging_react_apps#exercises-1-6-1-14) besides those found below. Do not submit your work until you have completed all of the exercises you want to submit for the part.

You may submit all the exercises of this course into the same repository, or use multiple repositories. If you submit exercises of different parts into the same repository, please use a sensible naming scheme for the directories.

One very functional file structure for the submission repository is as follows:
```bash
part0
part1
    courseinfo
    unicafe
    anecdotes
part2
    courseinfo
    phonebook
    countries
```
See this [example submission repository](https://github.com/fullstack-hy2020/example-submission-repository)!

For each part of the course, there is a directory, which further branches into directories containing a series of exercises, like "unicafe" for part 1.

Most of the exercises of the course build a larger application, eg. courseinfo, unicafe and anecdotes in this part, bit by bit. It is enough to submit the completed application. You can make a commit after each exercise, but that is not compulsory. For example the course info app is built in exercises 1.1.-1.5. It is just the end result after 1.5 that you need to submit!

For each web application for a series of exercises, it is recommended to submit all files relating to that application, except for the directory node_modules.

## Exercise 1.1: Course Information, Step 1
_The application that we will start working on in this exercise will be further developed in a few of the following exercises. In this and other upcoming exercise sets in this course, it is enough to only submit the final state of the application. If desired, you may also create a commit for each exercise of the series, but this is entirely optional._

Use Vite to initialize a new application. Modify main.jsx to match the following
```javascript
import ReactDOM from 'react-dom/client'

import App from './App'

ReactDOM.createRoot(document.getElementById('root')).render(<App />)
```

and App.jsx to match the following

```javascript
const App = () => {
  const course = 'Half Stack application development'
  const part1 = 'Fundamentals of React'
  const exercises1 = 10
  const part2 = 'Using props to pass data'
  const exercises2 = 7
  const part3 = 'State of a component'
  const exercises3 = 14

  return (
    <div>
      <h1>{course}</h1>
      <p>
        {part1} {exercises1}
      </p>
      <p>
        {part2} {exercises2}
      </p>
      <p>
        {part3} {exercises3}
      </p>
      <p>Number of exercises {exercises1 + exercises2 + exercises3}</p>
    </div>
  )
}

export default App
```

and remove the extra files _App.css_ and _index.css_, also remove the directory assets.

Unfortunately, the entire application is in the same component. Refactor the code so that it consists of three new components: _Header, Content, and Total_. All data still resides in the _App_ component, which passes the necessary data to each component using props. _Header_ takes care of rendering the name of the course,_ Content_ renders the parts and their number of exercises and _Total_ renders the total number of exercises.

Define the new components in the file _App.jsx_.

The _App_ component's body will approximately be as follows:

```javascript
const App = () => {
  // const-definitions

  return (
    <div>
      <Header course={course} />
      <Content ... />
      <Total ... />
    </div>
  )
}
```

**WARNING** Don't try to program all the components concurrently, because that will almost certainly break down the whole app. Proceed in small steps, first make e.g. the component Header and only when it works for sure, you could proceed to the next component.

Careful, small-step progress may seem slow, but it is actually by far the fastest way to progress. Famous software developer Robert "Uncle Bob" Martin has stated

> _"The only way to go fast, is to go well"_

that is, according to Martin, careful progress with small steps is even the only way to be fast.

### Solution!
```javascript
const Header = (props) => {
  return(
    <h1>{props.course}</h1>
  )
}

const Content = (props) => {
  return(
    <>
      <p>
        {props.p1} {props.e1}
      </p>
      <p>
        {props.p2} {props.e2}
      </p>
      <p>
        {props.p3} {props.e3}
      </p>
    </>
  )
}

const Total = (props) => {
  return(
    <p>Number of exercises {props.e1 + props.e2 + props.e3}</p>
  )
}

const App = () => {
  const course = 'Half Stack application development'
  const part1 = 'Fundamentals of React'
  const exercises1 = 10
  const part2 = 'Using props to pass data'
  const exercises2 = 7
  const part3 = 'State of a component'
  const exercises3 = 14

  return (
    <div>
      <Header course={course} />
      <Content p1={part1} p2={part2} p3={part3} e1={exercises1} e2={exercises2} e3={exercises3} />
      <Total e1={exercises1} e2={exercises2} e3={exercises3} />
    </div>
  )
}

export default App
```
## Exercise 1.2: Course Information, Step 2
Refactor the _Content_ component so that it does not render any names of parts or their number of exercises by itself. Instead, it only renders three _Part_ components of which each renders the name and number of exercises of one part.

```javascript
const Content = ... {
  return (
    <div>
      <Part .../>
      <Part .../>
      <Part .../>
    </div>
  )
}
```
### Solution!
```javascript
const Header = (props) => {
  return(
    <h1>{props.course}</h1>
  )
}

const Part = (props) => {
  return (
    <p>
      {props.part} {props.exercises}
    </p>
  )
}

const Content = (props) => {
  return(
    <div>
      <Part part={props.p1} exercises={props.e1}/>
      <Part part={props.p2} exercises={props.e2}/>
      <Part part={props.p3} exercises={props.e3}/>
    </div>
  )
}

const Total = (props) => {
  return(
    <p>Number of exercises {props.e1 + props.e2 + props.e3}</p>
  )
}

const App = () => {
  const course = 'Half Stack application development'
  const part1 = 'Fundamentals of React'
  const exercises1 = 10
  const part2 = 'Using props to pass data'
  const exercises2 = 7
  const part3 = 'State of a component'
  const exercises3 = 14

  return (
    <div>
      <Header course={course} />
      <Content p1={part1} p2={part2} p3={part3} e1={exercises1} e2={exercises2} e3={exercises3} />
      <Total e1={exercises1} e2={exercises2} e3={exercises3} />
    </div>
  )
}

export default App
```
