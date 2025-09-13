---
title: "Capstone Projects"
description: "Real-world projects to showcase your skills and build your portfolio"
date: 2024-01-15T16:33:54+02:00
lastmod: 2024-01-15T16:33:54+02:00
draft: false
---

# Capstone Project: VueTasks

## Overview

The capstone project is a comprehensive task management application called **VueTasks** that students will develop throughout the semester. This project serves as the culminating experience of the Web Application Development course, demonstrating mastery of Vue.js, TypeScript, and modern web development practices.

## Project Timeline

- **Project Kickoff**: Week 3 (January 29 - February 2, 2024)
- **Development Phase**: Weeks 3-11 (January 29 - March 30, 2024)
- **Final Submission**: Week 11 (March 30, 2024)
- **Final Exam**: Week 15 (April 25, 2024)

## Project Requirements

### Technical Requirements
- **Frontend**: Vue.js 3 with Composition API
- **TypeScript**: Full TypeScript integration with proper typing
- **Build Tool**: Vite for development and production builds
- **State Management**: Pinia for global state management
- **Routing**: Vue Router with multiple pages
- **Styling**: CSS framework or custom CSS
- **Testing**: Vitest + Vue Test Utils (minimum 3 tests)
- **Deployment**: Live application on Netlify or Vercel

### Functional Requirements
- **Task Management**: Create, read, update, delete tasks
- **Categories**: Organize tasks by categories
- **Search/Filter**: Search and filter functionality
- **Form Validation**: VeeValidate for form validation
- **Loading States**: Proper loading and error handling
- **Responsive Design**: Mobile-first approach
- **Performance**: Optimized with lazy loading

## VueTasks Application Features

### Core Features
- **Task CRUD**: Create, edit, delete, and mark tasks as complete
- **Category Management**: Organize tasks by categories (Work, Personal, Shopping, etc.)
- **Search & Filter**: Search tasks by title and filter by status/category
- **Responsive Design**: Works seamlessly on desktop and mobile devices
- **Form Validation**: Comprehensive form validation using VeeValidate
- **Loading States**: Proper loading indicators and error handling
- **Modal Dialogs**: Create/edit tasks in modal dialogs using Teleport
- **Transitions**: Smooth animations and transitions
- **Testing**: Unit tests for components and composables

## Capstone Milestones (W3 → W11)

### W3: Kickoff — Navigation + Empty Views
- **Deliverable**: Repository setup, folder structure, Router wired, navigation + empty views
- **Requirements**:
  - Create GitHub repository with proper naming convention
  - Set up Vue.js 3 + TypeScript + Vite project
  - Configure Vue Router with basic routes (Home, About, Tasks)
  - Create navigation component with router-links
  - Set up basic layout with empty view components

### W4: List View from Mock Data
- **Deliverable**: List view rendering from mock data
- **Requirements**:
  - Create mock task data structure
  - Implement task list component with v-for
  - Display tasks with proper keys
  - Basic task item component with title, description, status
  - Responsive grid/list layout

### W5: Pinia Wired — State Management
- **Deliverable**: Pinia wired; tasks read from store; basic add/remove actions
- **Requirements**:
  - Set up Pinia store with TypeScript
  - Define task state, getters, and actions
  - Connect components to store
  - Implement add task functionality
  - Implement remove/delete task functionality
  - Basic task status toggle (complete/incomplete)

### W6: API Integration + Loading/Error UX
- **Deliverable**: Switch data to mock/public API; loading/error UX in Tasks
- **Requirements**:
  - Replace mock data with API calls (fetch or Axios)
  - Implement loading states with Suspense
  - Add error handling and error components
  - Loading indicators for async operations
  - Proper error messages and fallbacks

### W7: Filters/Search & Categories
- **Deliverable**: Filters/search & categories implemented
- **Requirements**:
  - Add search functionality (filter by task title)
  - Implement category filtering
  - Add computed properties for filtered results
  - Category management (add, edit, delete categories)
  - Search input with debouncing
  - Filter UI components

### W8: Validated Forms Across CRUD
- **Deliverable**: Validated forms across CRUD (create/edit)
- **Requirements**:
  - Install and configure VeeValidate
  - Create task form with validation rules
  - Edit task functionality with pre-filled forms
  - Form accessibility and focus management
  - Custom validation rules for task requirements
  - Error display and user feedback

### W9: Modal + Transitions + Optional Tabs
- **Deliverable**: Modal + transitions + (optional) tabs integrated into VueTasks
- **Requirements**:
  - Implement modal dialogs using Teleport
  - Create/edit tasks in modal dialogs
  - Add smooth transitions and animations
  - Focus trap for accessibility
  - Optional: Tabbed interface with keep-alive
  - Transition effects for list updates

### W10: Unit Tests Passing
- **Deliverable**: Unit tests passing (min 3) + one router/store test
- **Requirements**:
  - Set up Vitest + Vue Test Utils
  - Write component tests for key components
  - Write composable tests for utility functions
  - Add router test for navigation
  - Add store test for state management
  - Achieve minimum 80% test coverage

### W11: Performance Pass + Deployed Preview
- **Deliverable**: Perf pass + deployed preview (final project deliverable)
- **Requirements**:
  - Implement lazy loading for routes
  - Optimize bundle size and performance
  - Deploy to Netlify or Vercel
  - Performance audit and optimization
  - Final code review and cleanup
  - Complete documentation and README

## Deliverables

### 1. Project Repository
- **GitHub Repository**: Well-organized code with proper documentation
- **README.md**: Comprehensive project documentation
- **Live Demo**: Deployed application accessible via URL
- **Commit History**: Regular, meaningful commits throughout development

### 2. Technical Documentation
- **Architecture Overview**: System design and component structure
- **API Documentation**: External APIs used and data flow
- **Setup Instructions**: How to run the project locally
- **Testing Strategy**: Testing approach and coverage

### 3. User Documentation
- **User Manual**: How to use the application
- **Feature Overview**: Key features and functionality
- **Screenshots**: Visual documentation of the application

### 4. Presentation
- **Live Demo**: 10-minute presentation of your application
- **Technical Walkthrough**: Code architecture and key features
- **Challenges and Solutions**: Problems faced and how you solved them
- **Future Enhancements**: Ideas for further development

## Grading Criteria

### Milestone Completion (60%)
- **W3-W11 Deliverables**: Each milestone worth 6% (9 milestones × 6% = 54%)
- **Final Deployment**: Working deployed application (6%)
- **Code Quality**: Clean, readable, and well-commented code throughout

### Technical Implementation (25%)
- **Vue.js 3 + TypeScript**: Proper use of Composition API and TypeScript
- **State Management**: Effective Pinia store implementation
- **Routing**: Proper Vue Router setup and navigation
- **Testing**: Minimum 3 unit tests + router/store tests
- **Performance**: Optimized with lazy loading and best practices

### User Experience (15%)
- **Design**: Professional and intuitive user interface
- **Responsiveness**: Works well on all device sizes
- **Accessibility**: Form validation, focus management, keyboard navigation
- **Interactions**: Smooth transitions, loading states, error handling

### Documentation (0% - Required but not graded)
- **README**: Clear setup and usage instructions
- **Code Comments**: Well-documented code
- **Deployment**: Live demo URL and setup instructions

## Resources and Support

### Development Tools
- **VS Code**: Recommended editor with Vue.js extensions
- **Vue DevTools**: Browser extension for debugging
- **GitHub**: Version control and collaboration
- **Figma**: Wireframing and design (free for students)

### APIs and Services
- **JSONPlaceholder**: Mock REST API for testing
- **Firebase**: Backend-as-a-Service for authentication and database
- **Supabase**: Open source Firebase alternative
- **Netlify/Vercel**: Free hosting for static sites

### Learning Resources
- **Vue.js Documentation**: Official Vue.js guide
- **Vue Mastery**: Video tutorials and courses
- **MDN Web Docs**: Web development reference
- **Stack Overflow**: Community support

### Office Hours
- **Monday**: 2:00 PM - 4:00 PM
- **Wednesday**: 10:00 AM - 12:00 PM
- **Friday**: 1:00 PM - 3:00 PM

## Submission Guidelines

### Repository Requirements
- **Naming**: `webdev-capstone-[your-username]`
- **Visibility**: Public repository
- **Organization**: Clear folder structure
- **Documentation**: Complete README.md

### Final Submission
1. **GitHub Repository**: Submit repository URL
2. **Live Demo**: Submit deployed application URL
3. **Documentation**: Submit all documentation files
4. **Presentation Slides**: Submit presentation materials

### Late Submission Policy
- **1-2 days late**: 10% penalty
- **3-5 days late**: 20% penalty
- **More than 5 days late**: 50% penalty
- **No submissions after April 25**: Zero grade

## Success Tips

### Planning
- Start early and plan thoroughly
- Break down the project into manageable tasks
- Set realistic milestones and deadlines
- Regular communication with team members (if applicable)

### Development
- Commit code regularly with meaningful messages
- Test features as you build them
- Keep the user experience in mind
- Document your code and decisions

### Presentation
- Practice your demo multiple times
- Prepare for technical questions
- Highlight your best features
- Be honest about challenges and limitations

## Previous Projects

### Spring 2023 Examples
- **E-Learning Platform**: Interactive course management system
- **Restaurant Management**: Table booking and menu management
- **Fitness Tracker**: Workout logging and progress tracking
- **Library Management**: Book catalog and borrowing system

### Key Learnings
- User experience is as important as technical implementation
- Proper planning saves time in the long run
- Testing early and often prevents major issues
- Documentation is crucial for project success

---

**Remember**: The capstone project is your opportunity to showcase everything you've learned in this course. Choose a project that excites you and challenges you to grow as a developer. Good luck!
