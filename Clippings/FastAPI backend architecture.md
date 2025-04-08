## FastAPI FOUNDATION

## Part 1: Blueprint

In this article, we will discuss two main strategies for structuring your FastAPI projects and highlight the scenarios in which each one is more suitable.

## Why Proper Structuring Matters?

Here are the most important reasons to structure your code based on best practices.

1. **Enhanced Scalability:***Well-organized code grows smoothly with your FastAPI project.*
2. **Improved Maintainability:***Easy-to-understand code makes updates and fixes simple.*
3. **Streamlined Collaboration:***Clear structure helps teams work together efficiently.*

Dall-E generated image with the following concept: An abstract software blueprint

## Key Principles for Structuring Projects

In building FastAPI applications, it’s crucial to follow these best practices:

1. **Separation of Concerns:***Separate different aspects of your FastAPI project, such as routes, models, and business logic, for clarity and maintainability.*
2. **Modularization:***Break down your FastAPI application into reusable modules to promote code reusability and organization.*
3. **Dependency Injection:***Decouple components by implementing dependency injection, which allows for more flexible and testable code in FastAPI using libraries like* `fastapi.Dependencies`*.*
4. **Testability:***Prioritize writing testable code in FastAPI applications by employing strategies like dependency injection and mocking to ensure robust testing and quality assurance.*

## Structuring Formats

FastAPI applications can be structured in different ways to accommodate various project needs.

There are two main approaches for structuring projects. One is based on file type and the other is based on module functionality.

## 1\. Structuring based on File-Type

In this approach, files are organized by type (e.g., API, CRUD, models, schemas, routers) as represented by [FastAPI itself](https://fastapi.tiangolo.com/tutorial/bigger-applications/).

This structure is more suitable for microservices or projects with fewer scopes:

```c
.
├── app  # Contains the main application files.
│   ├── __init__.py   # this file makes "app" a "Python package"
│   ├── main.py       # Initializes the FastAPI application.
│   ├── dependencies.py # Defines dependencies used by the routers
│   ├── routers
│   │   ├── __init__.py
│   │   ├── items.py  # Defines routes and endpoints related to items.
│   │   └── users.py  # Defines routes and endpoints related to users.
│   ├── crud
│   │   ├── __init__.py
│   │   ├── item.py  # Defines CRUD operations for items.
│   │   └── user.py  # Defines CRUD operations for users.
│   ├── schemas
│   │   ├── __init__.py
│   │   ├── item.py  # Defines schemas for items.
│   │   └── user.py  # Defines schemas for users.
│   ├── models
│   │   ├── __init__.py
│   │   ├── item.py  # Defines database models for items.
│   │   └── user.py  # Defines database models for users.
│   ├── external_services
│   │   ├── __init__.py
│   │   ├── email.py          # Defines functions for sending emails.
│   │   └── notification.py   # Defines functions for sending notifications
│   └── utils
│       ├── __init__.py
│       ├── authentication.py  # Defines functions for authentication.
│       └── validation.py      # Defines functions for validation.
├── tests
│   ├── __init__.py
│   ├── test_main.py
│   ├── test_items.py  # Tests for the items module.
│   └── test_users.py  # Tests for the users module.
├── requirements.txt
├── .gitignore
└── README.md
```

## In this structure

- `app/`: Contains the main application files.
- `main.py`: Initializes the FastAPI application.
- `dependencies.py`: Defines dependencies used by the routers.
- `routers/`: Contains router modules.
- `crud/`: Contains CRUD (Create, Read, Update, Delete) operation modules.
- `schemas/`: Contains Pydantic schema modules.
- `models/`: Contains database model modules.
- `external_services/`: Contains modules for interacting with external services.
- `utils/`: Contains utility modules.
- `tests/`: Contains test modules.

## 2\. Structuring based on Module-Functionality

In the second approach, we organize our files based on package functionality for example authentication sub-package, users sub-package, and posts sub-package.

The module-functionality structure is better suited for monolithic projects containing numerous domains and modules. By grouping all file types required by a single sub-package, it improves development efficiency.

This structure is suggested by the [fastapi-best-practices](https://github.com/zhanymkanov/fastapi-best-practices#1-project-structure-consistent--predictable) GitHub repository.

In this structure, Each package has its own router, schemas, models, etc.

```c
fastapi-project
├── alembic/
├── src
│   ├── auth
│   │   ├── router.py         # auth main router with all the endpoints
│   │   ├── schemas.py        # pydantic models
│   │   ├── models.py         # database models
│   │   ├── dependencies.py   # router dependencies
│   │   ├── config.py         # local configs
│   │   ├── constants.py      # module-specific constants
│   │   ├── exceptions.py     # module-specific errors
│   │   ├── service.py        # module-specific business logic
│   │   └── utils.py          # any other non-business logic functions
│   ├── aws
│   │   ├── client.py  # client model for external service communication
│   │   ├── schemas.py
│   │   ├── config.py
│   │   ├── constants.py
│   │   ├── exceptions.py
│   │   └── utils.py
│   └── posts
│   │   ├── router.py
│   │   ├── schemas.py
│   │   ├── models.py
│   │   ├── dependencies.py
│   │   ├── constants.py
│   │   ├── exceptions.py
│   │   ├── service.py
│   │   └── utils.py
│   ├── config.py      # global configs
│   ├── models.py      # global database models
│   ├── exceptions.py  # global exceptions
│   ├── pagination.py  # global module e.g. pagination
│   ├── database.py    # db connection related stuff
│   └── main.py
├── tests/
│   ├── auth
│   ├── aws
│   └── posts
├── templates/
│   └── index.html
├── requirements
│   ├── base.txt
│   ├── dev.txt
│   └── prod.txt
├── .env
├── .gitignore
├── logging.ini
└── alembic.ini
```

## In this structure

Store all domain directories inside `src` folder.

1. `src/`: The highest level of an app, contains common models, configs, and constants, etc.
2. `src/main.py`: Root of the project, which inits the FastAPI app

Each package has its own router, schemas, models, etc.

1. `router.py`: is the core of each module with all the endpoints
2. `schemas.py`: for pydantic models
3. `models.py`: for database models
4. `service.py`: module-specific business logic
5. `dependencies.py`: router dependencies
6. `constants.py`: module-specific constants and error codes
7. `config.py`: e.g. env vars
8. `utils.py`: non-business logic functions, e.g. response normalization, data enrichment, etc.
9. `exceptions.py`: module-specific exceptions, e.g. `PostNotFound`, `InvalidUserData`

When a package requires services or dependencies or constants from other packages, import them with an explicit module name to avoid ambiguity.

```c
from src.auth import constants as auth_constants
from src.notifications import service as notification_service
from src.posts.constants import ErrorCode as PostsErrorCode  # in case we have Standard ErrorCode in constants module of each package
```

## Finally

In conclusion, structuring your FastAPI projects is essential for maintaining scalability, readability, and maintainability as your application grows. By organizing your code effectively, you ensure that it remains manageable and adaptable to evolving requirements.

We discussed two main types of structuring FastAPI projects: the file-type structure and the module-functionality structure.

The file-type structure, represented by FastAPI itself, organizes files based on their type (e.g., routers, schemas, models). This structure is suitable for microservice architectures where individual services have single responsibilities.

On the other hand, the module-functionality structure separates files based on module functionality rather than file type. This approach is more suitable for larger monolithic applications, promoting better organization and maintainability.

In choosing the right structure for your FastAPI project, consider factors such as project size, complexity, and architectural design. Ultimately, whether you opt for the file-type structure or the module functionality structure, prioritizing organization and clarity will contribute to the long-term success of your FastAPI applications.

## Resources

Bigger Applications - Multiple Files - FastAPI

### FastAPI framework, high performance, easy to learn, fast to code, ready for production

fastapi.tiangolo.com

[View original](https://fastapi.tiangolo.com/tutorial/bigger-applications/?source=post_page-----0219a6600a8f---------------------------------------)GitHub - zhanymkanov/fastapi-best-practices: FastAPI Best Practices and Conventions we used at our…

### FastAPI Best Practices and Conventions we used at our startup - zhanymkanov/fastapi-best-practices

github.com

[View original](https://github.com/zhanymkanov/fastapi-best-practices?source=post_page-----0219a6600a8f---------------------------------------#1-project-structure-consistent--predictable)