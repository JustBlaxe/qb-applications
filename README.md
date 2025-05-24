# QB-Applications

A comprehensive job application system for QBCore framework. This resource allows players to apply for whitelisted jobs and enables job managers to review applications, manage hiring status, and customize application questions.

![QB-Applications](https://sdmntprukwest.oaiusercontent.com/files/00000000-a0b0-6243-9611-a2f114858006/raw?se=2025-05-24T13%3A25%3A51Z&sp=r&sv=2024-08-04&sr=b&scid=418ea3d8-4b4f-5707-bf5b-4040617ef8c0&skoid=0a4a0f0c-99ac-4752-9d87-cfac036fa93f&sktid=a48cca56-e6da-484e-a814-9c849652bcb3&skt=2025-05-24T10%3A30%3A37Z&ske=2025-05-25T10%3A30%3A37Z&sks=b&skv=2024-08-04&sig=xjwIYofdEwk3HzEyy7l51KR20AmsAHJH3nhsSdR/NDk%3D)

## Features

- **Player Features:**

  - Apply for whitelisted jobs through an intuitive UI
  - View application status (pending, approved, denied)
  - Reapply for jobs if a previous application was denied
  - Interact with a customizable NPC to access the application system

- **Manager Features:**

  - Review pending applications
  - Approve or deny applications with notifications to applicants
  - Toggle hiring status for jobs
  - Customize application questions with different input types (textarea, radio buttons, etc.)
  - Filter applications by status (pending, approved, denied)

- **Technical Features:**
  - Clean and responsive UI
  - Full database integration with MySQL
  - Clipboard prop and animations for immersion
  - Easy configuration via config.lua
  - Multi-language support (locale system)
  - Target system integration for NPC interaction

## Dependencies

- [qb-core](https://github.com/qbcore-framework/qb-core)
- [oxmysql](https://github.com/overextended/oxmysql)
- [qb-target](https://github.com/qbcore-framework/qb-target) (optional, for NPC interaction)

## Installation

1. Download the resource and place it in your server's resources folder
2. Add `ensure qb-applications` to your server.cfg
3. Restart your server or start the resource

The resource will automatically create all necessary database tables on first start.

## Configuration

### Adding Jobs

Edit the `config.lua` file to add jobs that should use the application system:

```lua
Config.Jobs = {
    ['lspd'] = {
        label = 'Los Santos Police Department',
        bossgrades = {4}, -- Grade levels that can manage applications
        hiring = true
    },
    ['ambulance'] = {
        label = 'Emergency Medical Services',
        bossgrades = {4},
        hiring = true
    }
    -- Add more jobs as needed
}
```

### Default Questions

You can customize the default questions that will be used for all jobs:

```lua
Config.DefaultQuestions = {
    {
        id = 1,
        question = "Why do you want to join this job?",
        type = "textarea",
        required = true
    },
    {
        id = 2,
        question = "What is your previous experience?",
        type = "textarea",
        required = true
    }
    -- Add more questions as needed
}
```

### NPC Configuration

Configure the application NPC's appearance and location:

```lua
Config.NPC = {
    enabled = true, -- Set to false to disable NPC and allow everyone to use command
    model = 'ig_paper', -- NPC model
    coords = vector4(81.7043, -887.6457, 35.0579, 328.2473), -- x, y, z, heading
    blip = {
        enabled = false,
        sprite = 280,
        color = 3,
        scale = 0.8,
        label = "Job Applications"
    },
    target = {
        label = "Apply for Jobs",
        icon = "fas fa-briefcase",
        distance = 2.0
    }
}
```

## Usage

### Player Commands

- `/apply` - Opens the job application UI (only works for managers if NPC is enabled)

### Job Application Process

1. Approach the job application NPC or use the `/apply` command
2. Select a job from the available list
3. Fill out the application form with your answers
4. Submit the application and wait for management review
5. Check the "My Applications" tab to see the status

### Manager Features

Job managers (players with job grades listed in the `bossgrades` config) can:

1. Access the "Manage Applications" tab to see all applications for their job
2. Review, approve, or deny applications
3. Use the "Job Settings" tab to enable/disable hiring
4. Customize application questions specific to their job

## Custom Question Types

The system supports the following question types:

- `textarea` - Multi-line text input
- `text` - Single line text input
- `radio` - Multiple choice (single selection)
- `select` - Dropdown selection
