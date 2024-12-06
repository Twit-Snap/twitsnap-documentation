# Postmortem

## What Went Well

### Planning

- The separation of roles and division of tasks was quite clear and effective regarding each person's knowledge.
- The defined timelines and objectives were successfully met.

### Technology

- React Native and Expo were a good choice for the app development as they allowed for cross-platform development and ease of implementation with a lower learning curve compared to other technologies.
- Node.js and Python were good choices for the services as both are languages that all team members had prior knowledge of and were easy to develop.

### Team Collaboration

- There was good communication and task assignment.
- Good use of communication and teamwork tools like Discord, GitHub, etc.
- Integration through pull requests.

### Project Reception

- Users and evaluators were very positive about the project.
- The app did not present any issues during the live presentation.

## What Went Wrong

### Scalability

Although the microservices architecture implemented was generally quite good, there were some features that, due to the development time for the project, we had to limit the complexity of the solution, for example:

- Notifications of trending topics, which notify all users of the app.
- In profile editing, if any data contained within the twit object was modified, this change could be queued to modify all twits of that user; this case was designed but not implemented.

![Feature Design](AsyncUserEdit.png)

### Design System

Overall, the UI/UX of the app remained quite consistent, but there was a lot of "Copy-Paste" between components since a design system was not defined where each component had a predefined design.

### Metrics and Graphs

The necessary graphs and metrics were implemented in the back office and app, but the graph libraries could have been better utilized for a better visualization experience.
