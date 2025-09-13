---
title: "GitHub Usage Policy"
description: "Guidelines for using GitHub for assignments and collaboration at Salahaddin University-Erbil"
date: 2024-01-15T16:33:54+02:00
lastmod: 2024-01-15T16:33:54+02:00
draft: false
---

# GitHub Usage Policy for Students

## Overview

This policy outlines the requirements and guidelines for using GitHub in the Web Application Development course at Salahaddin University-Erbil. All students are required to use GitHub for submitting assignments, collaborating on projects, and maintaining their code portfolios.

## Account Setup

### Required Actions
1. **Create a GitHub Account**: If you don't have one, create a free account at [github.com](https://github.com)
2. **Use University Email**: Use your university email address for your GitHub account
3. **Professional Username**: Choose a professional username that includes your name or student ID
4. **Complete Profile**: Add a professional profile picture and bio

### Account Verification
- Submit your GitHub username to the instructor by the end of Week 1
- Your account will be verified and added to the course organization

## Repository Naming Convention

### Assignment Repositories
All assignment repositories must follow this naming pattern:
```
webdev-assignment-[number]-[your-username]
```

**Examples:**
- `webdev-assignment-1-polla-fattah`
- `webdev-assignment-2-ahmed-mohammed`
- `webdev-assignment-3-sara-ahmed`

### Capstone Project Repository
```
webdev-capstone-[your-username]
```

## Repository Structure

### Required Files
Every repository must include:

1. **README.md** - Project description and setup instructions
2. **LICENSE** - MIT License (recommended)
3. **.gitignore** - Appropriate for your project type
4. **package.json** - For Node.js projects (if applicable)

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

## Submission Guidelines

### Assignment Submission Process
1. **Create Repository**: Use the naming convention above
2. **Push Code**: Commit and push all code to the repository
3. **Create Pull Request**: Submit a pull request to the course organization
4. **Add Labels**: Use appropriate labels (assignment, week-1, etc.)
5. **Notify Instructor**: Send email with repository link

### Commit Message Standards
Use clear, descriptive commit messages:

**Good Examples:**
- `feat: add user authentication system`
- `fix: resolve responsive design issues on mobile`
- `docs: update README with setup instructions`
- `style: improve button hover effects`

**Bad Examples:**
- `update`
- `fix`
- `changes`
- `asdf`

### Branch Strategy
- **Main Branch**: Keep stable, working code
- **Feature Branches**: Use for new features (`feature/user-auth`)
- **Bug Fixes**: Use for bug fixes (`bugfix/login-error`)

## Collaboration Guidelines

### Group Projects
- One student creates the repository
- Add all team members as collaborators
- Use issues and project boards for task management
- Each team member should have meaningful commits

### Code Review Process
1. **Self-Review**: Review your own code before submitting
2. **Peer Review**: Review at least one classmate's code per week
3. **Instructor Review**: Instructor will review all submissions

### Communication
- Use GitHub Issues for questions and discussions
- Tag the instructor (@instructor-username) for urgent matters
- Use descriptive issue titles and labels

## Academic Integrity

### Original Work
- All code must be your original work
- You may reference tutorials and documentation
- Cite any external resources in your README

### Collaboration vs. Cheating
**Allowed:**
- Discussing concepts and approaches
- Helping with debugging
- Sharing resources and tutorials
- Code review and feedback

**Not Allowed:**
- Copying entire code solutions
- Sharing assignment solutions
- Using code from previous semesters
- Plagiarizing from online sources

### Consequences
Violations of academic integrity will result in:
- First offense: Warning and re-submission required
- Second offense: Zero grade for the assignment
- Third offense: Course failure

## Privacy and Security

### Sensitive Information
**Never commit:**
- Passwords or API keys
- Personal information
- University credentials
- Database connection strings

### Environment Variables
Use `.env` files for sensitive configuration:
```bash
# .env (add to .gitignore)
API_KEY=your_secret_key
DATABASE_URL=your_database_url
```

## Grading Criteria

### Repository Quality (20%)
- Proper naming convention
- Complete README.md
- Appropriate .gitignore
- Clean commit history

### Code Quality (40%)
- Working, functional code
- Clean, readable code
- Proper commenting
- Error handling

### Documentation (20%)
- Clear setup instructions
- Feature descriptions
- Live demo link
- Code comments

### Git Usage (20%)
- Meaningful commit messages
- Appropriate branching
- Regular commits
- Clean history

## Support and Resources

### Getting Help
- **Office Hours**: Monday 2-4 PM, Wednesday 10-12 PM, Friday 1-3 PM
- **GitHub Issues**: Use course repository issues for questions
- **Email**: [instructor-email@university.edu]

### Learning Resources
- [Git Handbook](https://guides.github.com/introduction/git-handbook/)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Markdown Guide](https://www.markdownguide.org/)
- [Vue.js Documentation](https://vuejs.org/guide/)

### Tools and Extensions
- **VS Code**: Recommended editor with Git integration
- **GitHub Desktop**: GUI for Git operations
- **GitKraken**: Advanced Git client
- **GitHub CLI**: Command-line interface

## Important Dates

- **GitHub Account Setup**: Due by January 22, 2024
- **First Assignment Submission**: January 29, 2024
- **Midterm Project**: March 15, 2024
- **Final Capstone Project**: April 16, 2024

## Contact Information

**Instructor**: [Instructor Name]
**Email**: [instructor-email@university.edu]
**Office**: Computer Science Department, Room 205
**GitHub**: [@instructor-username]

**Teaching Assistant**: [TA Name]
**Email**: [ta-email@university.edu]
**GitHub**: [@ta-username]

---

*This policy is subject to updates. Students will be notified of any changes via email and course announcements.*
