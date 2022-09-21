# Workshop material

## 1. Introduction (5 min)

- The point of this workshop is to show and explain some common Modern JavaScript patterns through an actual example
- Let's build an app and work through that
- Why and when would you need/want to use a frontend framework (mention htmx as a good middle ground)
- For our example, let's pretend we want an app for taking notes through this DjangoCon

## 2. Basic example (15 min)

- We have an empty index.html to start with (step-0)
- Let's grab json for talks
- Let's use Vue.js to display these talks
    - First get the auditorum talks
    - Then use for-loop to display
    - Then filter out talks without speakers
- Let's add Tailwind CSS to make it a bit nicer
- Let's add a second column, to display talk details
    - Let's have a button that selects a talk to display
    - Add a method to display the talk
    - Add information about speakers
    - Notice the duplicated code -> How do we avoid it?
    - Let's add a computed method
    - Let's add a link back to pretalx (step-1)

## 3. Store action (5 min)

- Change styling a bit (step-1)
- Add textarea to store the notes
- Note that it doesn't work. Why is that?
- Add two-way binding
- Replace with v-model
- Add "notes taken" section to show how state is shared and is reactive
- What problem are we starting to have? (step-2)

## 4. Add structure (15 min)

- This is not production ready and it's not realistic (it's lacking structure)
    - We're using development builds (both Vue and TailwindCSS)
    - We've put everything in one file
- Before we look at solutions let's compare to the world of Django
    - When we set up a Django project, it will run on one machine, where we can control the Python version, the system dependencies, etc.
    - Our JavaScript code will run on countless combinations of browsers, operating systems and machines
    - This means that we have quite a few more things to worry about when we consider our JavaScript code compared to our Python code
- To address many of these problems (and in order to encourage adoption of latest JavaScript features), a lot of the tooling we know today was born
    - We have bundlers, transpilers, minifiers, polyfills, and so many other things
    - An important thing to note here is that while there are way too many options and projects, it's getting better and better every day.
    - There are many projects today, that are aware not only of the technical issues they're trying to solve, but also of how difficult it is for someone just getting started to start using these tools. And they are making sure that this won't be the case anymore.
- This used to be one of the most frustrating parts (in a way still is), but it's gotten so much better
- Let's look at Vue's official docs of what's the proper way to set up a project (not just use CDN the way we did now)
- Let's move our app to a .vue file
- Let's add Tailwind (notice how the process is similar to adding a package to Django)
- Let's extract TalkItem into a separate component (step-3)

## 5. Add API calls (5 min)

- Instead of hardcoding talks.json, let's fetch it

## 6. Outro and questions (5 min)

- The ecosystem is huge, but much easier to navigate than it used to be
- The concepts we talked about are used in most other frontend frameworks as well
- Where to go from here
