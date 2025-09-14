---
title: "Assignments"
description: "Hands-on exercises and coding assignments to practice skills"
date: 2024-01-15T16:33:54+02:00
lastmod: 2024-01-15T16:33:54+02:00
draft: false
---

# Weekly Lab Activities

## Overview

Weekly lab activities are hands-on exercises designed to reinforce the concepts covered in each week's lectures. These activities build upon each other and prepare you for the capstone project milestones. All lab work must be submitted via GitHub following the [GitHub Policy](/github-policy/).

## Lab Activity Schedule

### W1 Lab: "Hello, Name!" + Counter
**Due**: September 13, 2025
**Topics**: TypeScript in Vue, SFC anatomy, reactivity primer

#### Requirements
- Create a Vue 3 + TypeScript project with Vite
- Build a "Hello, [Name]!" component with typed props
- Implement a counter component with typed state
- Run `vue-tsc` check to ensure type safety

#### Deliverables
- GitHub repository: `webdev-lab-1-[your-username]`
- Working Vue components with TypeScript
- TypeScript configuration and type checking

---

### W2 Lab: Reusable Card with Slots
**Due**: September 20, 2025
**Topics**: Props & emits (typed contracts), slots (named & scoped)

#### Requirements
- Create a reusable `Card` component with slots
- Implement named and scoped slots
- Build child→parent communication with typed emits
- Demonstrate slot flexibility with different content

#### Deliverables
- GitHub repository: `webdev-lab-2-[your-username]`
- Reusable Card component with proper typing
- Examples of slot usage

---

### W3 Lab: Multi-page Scaffold
**Due**: September 27, 2025
**Topics**: Vue Router, static/dynamic/nested routes, layouts

#### Requirements
- Set up Vue Router with basic routes
- Create Home, About, and Tasks pages
- Implement navigation with `<router-link>`
- Set up basic layout structure

#### Deliverables
- GitHub repository: `webdev-lab-3-[your-username]`
- Multi-page application with routing
- Navigation component

---

### W4 Lab: Login Form + Mini Todo
**Due**: October 4, 2025
**Topics**: Templates/directives, v-model, event handling

#### Requirements
- Create a login form with validation
- Build a mini todo list with proper keys
- Implement v-model for form inputs
- Demonstrate v-if/v-show, v-for with keys

#### Deliverables
- GitHub repository: `webdev-lab-4-[your-username]`
- Login form with validation
- Mini todo application

---

### W5 Lab: Shopping Cart Pattern
**Due**: October 11, 2025
**Topics**: Pinia stores, state management, computed properties

#### Requirements
- Set up Pinia store with TypeScript
- Create shopping cart functionality
- Implement computed totals
- Demonstrate state sharing across components

#### Deliverables
- GitHub repository: `webdev-lab-5-[your-username]`
- Shopping cart with Pinia store
- Computed properties and state management

---

### W6 Lab: API Integration with Loading/Error
**Due**: October 18, 2025
**Topics**: fetch/Axios, onMounted, Suspense, error handling

#### Requirements
- Pull posts from a public API (JSONPlaceholder)
- Implement loading states with Suspense
- Add error handling and error components
- Demonstrate async data fetching patterns

#### Deliverables
- GitHub repository: `webdev-lab-6-[your-username]`
- API integration with proper error handling
- Loading states and Suspense implementation

---

### W7 Lab: Filtered & Categorized Task Board
**Due**: October 25, 2025
**Topics**: computed for search/filter, watch vs watchEffect

#### Requirements
- Create a task board with categories
- Implement search functionality with computed
- Add category filtering
- Demonstrate watch vs watchEffect patterns

#### Deliverables
- GitHub repository: `webdev-lab-7-[your-username]`
- Task board with filtering and search
- Computed properties and watchers

---

### W8 Lab: Validated Forms with Focus Management
**Due**: November 1, 2025
**Topics**: VeeValidate, custom rules, form accessibility

#### Requirements
- Install and configure VeeValidate
- Create validated create/edit forms
- Implement focus management for accessibility
- Add custom validation rules

#### Deliverables
- GitHub repository: `webdev-lab-8-[your-username]`
- Forms with VeeValidate integration
- Accessibility features and focus management

---

### W9 Lab: Accessible Modal + Transitions
**Due**: November 8, 2025
**Topics**: Teleport, keep-alive, lifecycle hooks, transitions

#### Requirements
- Create accessible modal using Teleport
- Implement focus trap for accessibility
- Add animated transitions
- Optional: Tabbed view with keep-alive

#### Deliverables
- GitHub repository: `webdev-lab-9-[your-username]`
- Modal with Teleport and accessibility
- Transitions and animations

---

### W10 Lab: Component & Composable Tests
**Due**: November 15, 2025
**Topics**: Vitest, Vue Test Utils, testing patterns

#### Requirements
- Set up Vitest + Vue Test Utils
- Write 2 component tests
- Write 1 composable test
- Add smoke route/store test

#### Deliverables
- GitHub repository: `webdev-lab-10-[your-username]`
- Test suite with component and composable tests
- Test configuration and setup

---

### W11 Lab: Performance + Deployment
**Due**: November 22, 2025
**Topics**: Lazy loading, bundle optimization, deployment

#### Requirements
- Add one lazy route
- Measure performance before/after
- Deploy to Netlify or Vercel
- Optimize bundle size

#### Deliverables
- GitHub repository: `webdev-lab-11-[your-username]`
- Deployed application with performance optimizations
- Performance metrics and deployment documentation

---

### W12 Lab: Refactoring + CI
**Due**: November 29, 2025
**Topics**: Debugging, refactoring, CI basics

#### Requirements
- Refactor a complex component for clarity
- Add a tiny CI step (optional)
- Improve code organization and readability
- Document refactoring decisions

#### Deliverables
- GitHub repository: `webdev-lab-12-[your-username]`
- Refactored code with improved organization
- CI configuration (if implemented)

---

### W13 Lab: Nuxt Sandbox OR Architecture Diagram
**Due**: December 6, 2025
**Topics**: SSR/SSG, Nuxt, architecture patterns

#### Requirements
- Create short Nuxt sandbox OR
- Design architecture diagram for VueTasks
- Explore SSR/SSG concepts
- Document architectural decisions

#### Deliverables
- GitHub repository: `webdev-lab-13-[your-username]`
- Nuxt sandbox or architecture documentation
- SSR/SSG exploration notes

---

### W14 Lab: Demo Rehearsal
**Due**: December 13, 2025
**Topics**: Project presentation, Q&A preparation

#### Requirements
- Dry-run demo of capstone project
- Prepare Q&A responses
- Review project documentation
- Practice presentation flow

#### Deliverables
- Updated capstone project repository
- Demo script and presentation notes
- Q&A preparation document

---

## Submission Guidelines

### Repository Requirements
- **Naming Convention**: `webdev-assignment-[number]-[your-username]`
- **Visibility**: Public repository
- **Organization**: Clear folder structure
- **Documentation**: Complete README.md

### README.md Template
```markdown
# Assignment [Number]: [Project Title]

## Description
Brief description of the project and its purpose.

## Features
- List of implemented features
- Key functionality

## Technologies Used
- Vue.js 3
- HTML5/CSS3
- JavaScript ES6+

## Setup Instructions
1. Clone the repository
2. Install dependencies: `npm install`
3. Run the project: `npm run dev`

## Live Demo
[Link to deployed application]

## Author
[Your Name] - [Your Student ID]
```

### Submission Process
1. **Create Repository**: Use proper naming convention
2. **Push Code**: Commit and push all code
3. **Deploy Application**: Set up live demo
4. **Update README**: Complete documentation
5. **Submit Link**: Send repository URL to instructor

## Grading and Feedback

### Lab Activity Grading
- **Weekly Activities**: 15% of final grade
- **Participation**: Active participation in labs and code reviews
- **Code Quality**: Clean, readable, and well-commented code
- **Completion**: All lab requirements met on time

### Grading Timeline
- **Lab Activities**: Graded within 1 week
- **Feedback**: Detailed comments on code and functionality
- **Participation**: Ongoing assessment throughout semester

### Late Submission Policy
- **1-2 days late**: 10% penalty
- **3-5 days late**: 20% penalty
- **More than 5 days late**: 50% penalty
- **No submissions after final deadline**: Zero grade

### Academic Integrity
- **Original Work**: All code must be your original work
- **Collaboration**: Discussion allowed, copying prohibited
- **Citations**: Credit any external resources used
- **Consequences**: See GitHub Policy for violations

## Support and Resources

### Getting Help
- **Office Hours**: Monday 2-4 PM, Wednesday 10-12 PM, Friday 1-3 PM
- **GitHub Issues**: Use course repository for questions
- **Email**: [instructor-email@university.edu]
- **Discord**: Course Discord server for quick questions

### Additional Resources
- **Assignment Templates**: Available in course repository
- **Code Examples**: Reference implementations provided
- **Tutorial Videos**: Step-by-step guides for complex topics
- **Peer Review**: Optional peer review sessions

---

*Remember: Assignments are designed to help you learn and practice. Don't hesitate to ask for help when you need it!*
