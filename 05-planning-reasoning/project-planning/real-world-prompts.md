# Real-World Prompts for Project Planning

This document provides practical examples of effective prompts to use during the planning phase of an agent-based coding project. These examples use a real-world case study of planning a "HomePulse" application.

## Case Study: HomePulse Application

The HomePulse application is a comprehensive building maintenance management system designed to track, schedule, and document maintenance activities for residential and commercial buildings. The application needs to handle:

- Property information management
- Maintenance task scheduling
- Service history tracking
- Document management
- User roles (property managers, maintenance staff, residents)
- Reporting and analytics

### Sample Property Data: Kuusitie 8

To make our prompts more concrete, we'll use sample data from a property called "Kuusitie 8":

**Basic Property Information:**
- Address: Kuusitie 8, 40520 Jyväskylä, Finland
- Originally built in 1982 with extension added in 1995
- Total area: 156 square meters
- Plot area: 1250 m²
- Building right: 300 m²

**Structural Elements:**
- Main building section (106 m²)
- L-shaped extension (50 m²)
- Rooms include: kitchen, living room, three bedrooms, bathroom, sauna, utility room, entryway

**Building Systems:**
- Heating: Ground source heat pump (NIBE, installed 2019), electric heaters, water-circulating floor heating, fireplace (installed 2008)
- Water: Complete plumbing renovation (2020), including water heater, pipes, fixtures
- Electrical: Main panel and distribution panel renovated (2020), wiring partially updated
- Envelope: Roof rebuilt with new underlay and metal sheeting (2016), cellulose insulation in attic (2012)

**Maintenance History:**
- Ventilation system installation (2008)
- Fireplace installation (2008)
- Basement waterproofing (2010)
- Drainage system renovation (2012)
- Roof replacement (2016)
- Living room and kitchen renovation (2017)
- Garage construction (2018)
- Ground source heat pump installation (2019)
- Major renovation due to water damage (2020-2021) including:
  - Floor structure replacement in bathroom and kitchen
  - Heating system upgrade
  - Plumbing system replacement
  - Electrical system modernization
  - Bathroom, utility room, and sauna renovation

**Incidents:**
- Water damage (October 15, 2020): Dishwasher leak affecting kitchen, utility room, and part of living room
- Roof leak (April 22, 2016): Damage to ceiling and wall in one bedroom, leading to full roof replacement

## Project Assessment Prompts

### Initial Project Exploration

```
I'm planning to build a HomePulse application using agent-based coding. The application will help property managers track maintenance activities, schedule tasks, and maintain documentation for residential and commercial buildings.

Key features include:
- Property information management
- Maintenance task scheduling
- Service history tracking
- Document management
- Different user roles (managers, maintenance staff, residents)
- Reporting and analytics

As an engineer orchestrating this project, I need to assess whether this is suitable for agent-based coding and identify the most appropriate areas for AI assistance. Please help me evaluate:

1. Which aspects of this project are most suitable for agent-based coding?
2. What potential challenges might arise specifically for this type of application?
3. What architectural patterns would you recommend considering?
4. How should I divide responsibilities between human engineers and AI agents?
```

### Technology Stack Assessment

```
For our HomePulse application, I'm considering the following technology stack:

- Frontend: React with TypeScript
- Backend: Node.js with Express
- Database: PostgreSQL
- Authentication: OAuth 2.0
- File Storage: AWS S3
- Hosting: AWS or Azure

As the engineer orchestrating this project, I need to evaluate how well this stack will work with agent-based coding approaches. Please analyze:

1. The suitability of each technology for AI agent assistance
2. Potential integration points for AI within this stack
3. Any alternative technologies I should consider that might work better with AI agents
4. Which parts of the stack would benefit most from agent-based development
```

## Architecture Planning Prompts

### Component Architecture Design

```
I need to design the component architecture for our HomePulse application. Based on our sample property "Kuusitie 8", the application will need to handle these main modules:

1. Property Management
   - Building basic information (address, construction year, area measurements)
   - Structural elements (main building, extensions, rooms)
   - Building systems inventory (heating, water, electrical, envelope)

2. Maintenance Management
   - Task scheduling (regular inspections, seasonal maintenance)
   - Maintenance history tracking (for activities like fireplace installations, roof replacements)
   - Major renovation project tracking (like the 2020-2021 comprehensive renovation)

3. Incident Tracking
   - Critical events documentation (water damage incidents)
   - Impact assessment (affected areas like in the 2020 dishwasher leak affecting multiple rooms)
   - Repair process tracking

4. Document Management
   - Inspection reports (like moisture measurements from 2020)
   - Building plans and blueprints
   - Warranty information and maintenance manuals

5. User Management
   - Different role types (property managers, maintenance staff, residents)
   - Permission controls for different data types
   - Notification preferences

6. Reporting & Analytics
   - Maintenance history visualization
   - Incident statistics
   - Cost tracking and forecasting

As the engineer leading this project, I want to design an architecture that is both modular and AI-friendly. Please help me create:

1. A high-level component diagram showing the main modules and their relationships
2. Clear interface definitions between components
3. A data flow diagram showing how information moves through the system
4. Specific recommendations for making this architecture optimal for agent-based coding
```

### Database Schema Design

```
For our HomePulse application, I need to design a database schema that will be implemented in PostgreSQL. The application needs to store detailed property information and maintenance history similar to our sample property "Kuusitie 8".

The database needs to handle:

1. Properties with detailed metadata, including:
   - Basic information (address, build year, area measurements, owner information)
   - Structural elements (building sections, room inventory)
   - Building systems (heating, water, electrical, envelope details)

2. Maintenance records with:
   - Dated maintenance activities (like the fireplace installation in 2004, roof replacement in 2014)
   - Major renovations with detailed sub-tasks (like the 2021-2022 renovation)
   - Maintenance tasks categorized by building system

3. Incident tracking for:
   - Water damage events (like the two incidents in 2021 and 2022)
   - Structural issues
   - System failures
   - Including affected areas, repair details, and related documentation

4. Document management for:
   - Inspection reports
   - Measurement documents (like moisture measurements)
   - Renovation plans
   - Warranty information

5. Users with different roles and permissions (property managers, maintenance staff, residents)

As the engineer orchestrating this project, I need a database schema that is well-structured and will work effectively with AI agents. Please help me design:

1. An entity-relationship diagram showing the main tables
2. Key fields for each table with appropriate data types
3. Relationship definitions between tables
4. Indexing recommendations for optimal performance
5. Considerations for making this schema work well with agent-based coding
```

## Workflow Design Prompts

### Development Workflow Planning

```
I'm establishing the development workflow for our Building Maintenance Log application using agent-based coding. As the engineer orchestrating this project, I need to create a workflow that balances AI assistance with human oversight.

Please help me design a workflow that covers:

1. Requirements gathering and task decomposition
2. Development stages from planning to deployment
3. Specific checkpoints where human engineers should review and approve AI work
4. Testing strategies appropriate for agent-generated code
5. Documentation processes that work well with AI assistance
6. Specific prompt templates we can use for common development tasks

The workflow should emphasize that engineers remain the orchestrators while leveraging AI for appropriate tasks.
```

### Task Delegation Strategy

```
For our Building Maintenance Log application, I need to create a task delegation strategy that clearly defines what work should be handled by human engineers versus AI agents.

As the engineer orchestrating this project, please help me:

1. Identify specific components or features that are well-suited for AI implementation
2. List tasks that should remain under direct human control
3. Create decision criteria for determining when to use AI versus human implementation
4. Suggest a collaborative approach for complex features that require both
5. Establish oversight mechanisms for AI-generated code

For context, the application includes property management, scheduling, document handling, and multi-role user management with various authorization levels.
```

## Security Planning Prompts

### Security Requirements Analysis

```
For our HomePulse application, I need to establish comprehensive security requirements and ensure they're properly implemented when using agent-based coding.

As the engineer orchestrating this project, please help me:

1. Identify the key security considerations for a property management application handling potentially sensitive data
2. Create a security requirements checklist specific to our application
3. Determine which security aspects require direct human implementation versus AI assistance
4. Establish a security review process for AI-generated code
5. Identify potential security risks specific to agent-based development for this type of application

The application will handle personal information, property details, maintenance records, and provide different access levels for property managers, maintenance staff, and residents.
```

### Data Protection Strategy

```
Our HomePulse application will store and process various types of data, including:
- Personal information (names, contact details)
- Property information (addresses, security details)
- Maintenance records
- Financial information (maintenance costs)
- Documents (warranties, certificates, manuals)

As the engineer orchestrating this project, I need a comprehensive data protection strategy that works well with agent-based coding.

Please help me create:

1. A data classification system for different sensitivity levels
2. Specific protection mechanisms for each data category
3. Access control recommendations 
4. Data retention and deletion policies
5. Special considerations for implementing these protections when using AI agents for development
```

## Project Kickoff Prompts

### Project Setup Instructions

```
I'm ready to start the HomePulse application and need to set up the initial project structure optimized for agent-based coding.

As the engineer orchestrating this project, please help me:

1. Create a directory structure that will organize our React frontend and Node.js backend effectively
2. Establish initial configuration files (.gitignore, tsconfig.json, package.json, etc.)
3. Set up an appropriate linting and formatting configuration
4. Create initial README documentation
5. Configure appropriate rules for AI agents if using Cursor IDE
6. Establish the repository structure with appropriate branch protection

Please provide specific code and configurations, not just high-level advice. The application will use TypeScript throughout, with React for frontend and Express for backend.
```

### Initial Development Tasks

```
Now that we've established the architecture and project structure for our HomePulse application, I need to create an initial task list for the first development sprint.

We'll be using our sample property "Kuusitie 8" as a test case during development, with all its real-world complexity:
- Multiple building systems (heating, electrical, water, envelope)
- Extensive maintenance history (2008-2020)
- Complex incident history (water damage events)
- Various structural elements (main building, extension, different room types)

As the engineer orchestrating this project, please help me:

1. Create a prioritized list of development tasks for the first sprint
2. Divide these tasks into those suitable for AI implementation vs. human implementation
3. Write specific user stories for the initial features
4. Create acceptance criteria for each task
5. Suggest a timeline for the first sprint
6. Identify the initial "quick wins" where AI can provide the most immediate value

The first sprint should focus on establishing the core architecture and basic property management functionality that could handle the complexity of our sample property.
```

## Using These Prompts Effectively

These example prompts demonstrate how to effectively guide AI agents during the project planning phase. Key principles include:

1. **Provide Clear Context**: Include enough background about the project for the AI to understand the domain.

2. **Specific Guidance**: Request specific outputs rather than general advice.

3. **Emphasize Orchestration**: Position yourself as the engineer orchestrating the AI, not just accepting its outputs.

4. **Request Structured Outputs**: Ask for diagrams, checklists, and organized information rather than prose.

5. **Include Domain Details**: Mention specific domain requirements that might impact design decisions.

6. **Request Multiple Options**: When appropriate, ask for alternatives to consider rather than a single solution.

7. **Focus on Practical Application**: Request information that can be directly applied to your project.

Remember that these prompts should be adapted to your specific project requirements and organizational standards. The engineer should always review, validate, and refine the AI's suggestions before proceeding with implementation.
