## **What are the two professional/career highlights you’re most proud of? Why?**
### Building the carbon reduction dashboard (align with my values, challenging, interaction with other teams)

### Building python scripts to speed up the matrix input in Gatwick model
Bypassing the VBA interface of the software and using the newer, less document python interface. Allowed to radically speed up the processing of origin/destination matrices. We were working on a large scale 24 hours model which used over 2,000 matrices. While the com interface work well in most cases this was too much for this use case and importing matrices through the COM interface was taking over 3 hours. 

Bypassing excel and processing / importing data through python reduced that process to just under 5 minutes. Took a few different step of optimisation (disable software UI updates, optimise order of import) But this allowed us to save a lot of time in the validation and calibration process which allowed us to deliver a much higher quality model. Ie with the time saving from the old import method we couid do an additional calibration run.

## **What’s one technical skill, not mentioned in the job ad, that you consider yourself to be very strong in? How would you use it at Doist?**

**2. System Optimization and Problem Solving**

- A key technical skill I bring is system optimization and iterative problem-solving. My background in transport modelling is centered around finding the most efficient solutions within a complex system. I'm used to working with constraints, evaluating trade-offs, and iteratively refining a design to achieve a specific goal, whether that's minimizing journey times in a city or maximizing the throughput of a junction. This involves a methodical approach to identifying bottlenecks, testing hypotheses, and validating results
- **How you'd use it at Doist:** "At Doist, I could apply this optimization mindset to the Todoist web app itself. I could analyze user workflows to identify areas of friction or inefficiency. For instance, if data shows users frequently abandon a particular task creation process, I could use my problem-solving skills to diagnose the issue, propose UI/UX changes, and then test those changes to see if they improve the user experience. My focus would be on making the app as smooth and efficient as possible for users."

**8. Abstraction and Conceptual Modeling**

- **What it is (for you):** Transport modelling _is_ abstraction. You're taking a complex, messy real-world system (a city's transportation network) and representing it in a simplified, manageable form. You're making decisions about what to include, what to exclude, and what level of detail is appropriate. You're translating real-world observations into mathematical relationships and algorithmic rules. This requires strong conceptual modeling skills – the ability to take a complex system and create a useful, simplified representation of it.
- **How it's phrased in the interview:** "A core technical skill I possess is abstraction and conceptual modeling. Transport modelling is fundamentally about creating simplified, yet representative, models of complex real-world systems. I'm skilled at identifying the essential elements of a transport network, translating those elements into a mathematical and algorithmic representation, and understanding the limitations of that abstraction. This involves making informed decisions about the level of detail required and the trade-offs between accuracy and computational cost."
- **How you'd use it at Doist:** "This ability to abstract and model complex systems is highly relevant to software development. When designing a new feature for Todoist, or even when refactoring existing code, I can apply this conceptual modeling skill to break down complex problems into smaller, manageable components. I can create clear and concise representations of the system's architecture, data flow, and user interactions. This helps in understanding the bigger picture, identifying potential bottlenecks, and designing elegant and efficient solutions. It’s about seeing the forest _and_ the trees."
## **Can you please share links to projects that you're proud of? These could include apps, portfolios, a GitHub profile and/or anything else that showcases your best work. (optional/can be replaced)**

### Draft
I'm really excited by the idea of using tech to solve everyday problems (especially my owns). Here are a couple of side projects that I think showcase this: 

First an iOS climbing app called Chalkr which I am currently working on. 
GitHub: [https://github.com/Portavion/Chalkr](https://github.com/Portavion/Chalkr)

I recently got into bouldering and I'm also a bit of a data geek. I love digging into stats to see how I can improve. I noticed most climbing apps were pretty basic when it came to real training insights when you compared to other apps like Strava or Garmin for running. I wanted something similar, that would let me see what I was doing in my climbing sessions and how my skills are improving. The app lets you easily log every climb – you can even snap a picture of the route and add all the relevant stats.  It tracks how long you're actually climbing on the wall versus resting.Which confirmed I was really bad at taking proper rests... It shows you how you ramp up the difficulty during a session. This helps me make sure I'm warming up properly and not jumping on hard stuff too soon and other useful stats. The app is local first as I wanted to be able to use it while climbing outside with limited signal. I'm currently working on the backend for sync and building a few more useful charts and stats.

I've used React Native and Expo, which was a great way to build for iOS  and continue to develop my React skills. I got to play around with creating custom components to display the data in a way that made sense for climbers. One key technical challenge was figuring out how to efficiently store and retrieve image data,keeping the UI feel smooth even with lots of route photos. I solved it by experimenting with expo image preloading and caching as well as generating a lower resolution thumbnail for each route picture. Which makes loading all route settings almost instantaneous.

Then, there is a quick web app, Velock, which I've built to quickly check the availability of several Santander Bike docking stations.
GitHub: https://github.com/Portavion/velock (which also has a quick demo)

I use the Santander Cycles in London all the time, but I was a little frustrated with their app. You can save favorite stations, but you can't organise them into different lists. And trying to search for a station by address was often a failure as I think they rely on the street road attached to the name of the docking station.

The app lets you create custom lists of stations – I have one for "Home," "Work," "Gym," etc. Makes it super quick to check availability. For the search I used a combination of OpenStreetMap's geocoding API and PostGIS, a spatial extension for PostgreSQL. Which gives more accurate results than the official app. It pulls real-time bike availability data from the TfL Open API. I've built it using Nodejs and Express for the backend with a PostgreSQL database. The frontend is built with React. It was fun getting to work with multiple APIs and integrate them into a single app. TfL Open API has an endpoint to search for docking stations but this only allows match on the station name, like the Santader app. An interesting challenge was implementing a better search feature. I've solved this by getting the coordinates of the input address using OpenStreetMap geocoding endpoint. Then leveraging PostGIS to calculate the shortest distance to each docking stations.

I hope you find these projects as interesting as I found building them. I'm excited at the possibility of bringing the same approach to Doist.
