# FastAPI FOUNDATION

## Part 1: Blueprint

### Key Principles for Structuring Projects

In building FastAPI applications, it’s crucial to follow these best practices:

1. **Separation of Concerns:** Separate different aspects of your FastAPI project, such as routes, models, and business logic, for clarity and maintainability.
2. **Modularisation:***Break down your FastAPI application into reusable modules to promote code reusability and organisation.*
3. **Dependency Injection:** Decouple components by implementing dependency injection, which allows for more flexible and testable code in FastAPI using libraries like `fastapi.Dependencies`.
4. **Testability:** Prioritise writing testable code in FastAPI applications by employing strategies like dependency injection and mocking to ensure robust testing and quality assurance.

### Structuring Formats

FastAPI applications can be structured in different ways to accommodate various project needs.

There are two main approaches for structuring projects. One is based on file type and the other is based on module functionality.

#### 1\. Structuring Based on File-Type

In this approach, files are organised by type (e.g., API, CRUD, models, schemas, routers) as represented by [FastAPI itself](https://fastapi.tiangolo.com/tutorial/bigger-applications/).

This structure is more suitable for microservices or projects with fewer scopes:

```
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

##### In This Structure

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

#### 2\. Structuring Based on Module-Functionality

In the second approach, we organize our files based on package functionality for example authentication sub-package, users sub-package, and posts sub-package.

The module-functionality structure is better suited for monolithic projects containing numerous domains and modules. By grouping all file types required by a single sub-package, it improves development efficiency.

This structure is suggested by the [fastapi-best-practices](https://github.com/zhanymkanov/fastapi-best-practices#1-project-structure-consistent--predictable) GitHub repository.

In this structure, Each package has its own router, schemas, models, etc.

```
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
##### In This Structure

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

```python
from src.auth import constants as auth_constants
from src.notifications import service as notification_service
from src.posts.constants import ErrorCode as PostsErrorCode  # in case we have Standard ErrorCode in constants module of each package
```
## Resources
 FastAPI Best Practices and Conventions we used at our startup - zhanymkanov/fastapi-best-practices
[View original](https://github.com/zhanymkanov/fastapi-best-practices?source=post_page-----0219a6600a8f---------------------------------------#1-project-structure-consistent--predictable)