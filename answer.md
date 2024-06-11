# Answer These Questions Here, you can add additional pages to answer questions, just link to them so that I can view these questions and see your answer or the link(s) to your answer.

## FastAPI and Pydantic

1. **What role does Pydantic play in FastAPI, and how does it enhance data validation and settings management?**
Pydantic provides data validation for our python projects. The most often used class is BaseModel, which is a superclass many of our data classes inherit from. These are the files on our project that use some part of the pydantic library. Usually, it is to extend from BaseModel, but also used for validation errors and related.
![Alt text](image.png)


2. **Outline the complete process of handling a user login request in your FastAPI application. Provide a step-by-step explanation with code examples from the project.**
The user is directed to the page with the login.html template. The user enters their credentials which are routed via the `@router.post` login_with_form to the UserService.login_user method, which blocks. That method is user_service.py.login_user which calls another method get_by_email and authenticates the session or not. If successful, the user is redirecetd to the /dashboard page and their access_token cookie is set.

3. **Explain the service repository pattern and how it is applied in your project. Provide an example of how routes are managed and linked to services.**
The repository pattern is a layer of abstraction between between the app and data. Instead of accessing data directly, the app goes thru the rest endpoints. Using a router is another example, where app state is signaled by accessing endpoints.

## Database Management with Alembic and SQLAlchemy

4. **How does Alembic manage database migrations, and why is this important for maintaining database schemas?**
Alembic pulls database jobs out of the database console and into the app developer's console. An example of a migration script is `docker compose exec fastapi alembic revision --autogenerate -m 'initial migration'`.

## Pytest

5. **Why is Pytest critical for the development of the API?**
Pytest confirms that parts of the code under test are functioning as expected. It also serves as documentation for features.

## JWT and User Authentication

6. **Explain the functioning of JWT (JSON Web Tokens) in user authentication. How are JWTs generated, encoded, and used within the project?**
JWTs are signed user credentials which are serialized. They are mostly used in the create_access_token and decode_token methods in our jwt_service module. They are used to curry user id, role, and expiration time. Here is encoding the token:
```
        encoded_jwt = jwt.encode(to_encode, settings.jwt_secret_key, algorithm=settings.jwt_algorithm)
        logging.info(f"JWT created with expiration at {expire.isoformat()}")
        logging.debug(f"Encoded JWT: {encoded_jwt}")
        
        # Immediate decoding test to verify correctness right after creation
        try:
            decoded = jwt.decode(encoded_jwt, settings.jwt_secret_key, algorithms=[settings.jwt_algorithm])
            logging.info("Immediate decode result: {}".format(decoded))
            logging.debug("Immediate decode check: {}".format(decoded))
        except jwt.ExpiredSignatureError:
            logging.error("Token already expired upon creation, check system clock.")
        except jwt.InvalidTokenError as e:
            logging.error(f"Token invalid right after creation: {e}")
        except jwt.PyJWTError as e:
            logging.error(f"Error during immediate token decode: {e}")
```

7. **Decode the following JWT and explain its contents:**
   - Token: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJqb2huLmRvZUBleGFtcGxlLmNvbSIsInJvbGUiOiJBRE1JTiIsInVzZXJfaWQiOiJjZGY4M2QzZi0zNzQ5LTRjZGQtOTRlYS1hNTVjZmMwNDhkMGYiLCJleHAiOjE3MTc2MTY4MjAuMjIwNzA5fQ.ANS8PgUiwPCmOvnZLYTCy_5WzLyhCDOx8aF4xu-Kaz8`
   Decodes to:
   ```
   {
   "sub": "john.doe@example.com",
   "role": "ADMIN",
   "user_id": "cdf83d3f-3749-4cdd-94ea-a55cfc048d0f",
   "exp": 1717616820.220709  /* Wednesday, June 5, 2024 7:47:00 PM */
   }
   ```

8. **Describe the user registration logic in your project. Provide a pseudo-code workflow from the registration request to storing the user in the database.**
The registration form captures the username, password, name, bio, pic, profile users, and role. Uses the browser's fetch api to post to the `/register/` endpoint. Router brokers the request to the async function `register` which makes another async request to the UserService.register_user method. Then to the `create` method in the same class, validates the request and sends a verification email which is handled by `EmailService`. 

9. **Detail the steps involved in the user email verification process. Provide a pseudo-code workflow from sending a verification email to activating the user's account.**
The link for the user to click in the email is `verification_url = f"{settings.server_base_url}verify-email/{user.id}/{user.verification_token}"`
which brings them back to the app to the `verify-email` endpoint. There, the UserService.verify_email_with_token method is called. that method tries to get the user by id and if successful, adds teh user to the session. The user is redirected to a successful landing page.

## Security Practices

10. **How do you ensure the security of user passwords in your project? Discuss the hashing algorithm used and any additional security measures implemented.**
The hashing algorithm in use for passwords here is bcrypt.

11. **Explain the difference between hashing and encoding. Provide examples from your project where each is used:**
    - **Hashing:** A one way trip for the data, but can be determined to be equal to another hashed data. See the `hash_password` and `verify_password` methods in the `security`` module.
    - **Encoding:** A conversion that can be undone, to place data into a state that suitable for trasfer or storage. An example is the data in a JWT token. See the `jwt_service` module here. 

## Project Management with Docker and CI/CD

12. **Discuss the advantages of using Docker Compose for running your project. How does it help in maintaining a consistent development and deployment environment?**
Using Docker helps manage large complicated projects made of multiple service. It keeps environments consistent by requiring the versions of dependencies. It also provides a way to build and push images to repositories in layers to save bandwidth and provide a convenient 3rd party storage location. Images can be tagged using semantic versioning, git ref, or other means.

13. **Describe the role of GitHub Actions in your project's CI/CD pipeline. How do you automate testing and deployment using GitHub Actions?**
GitHub actions are build steps that can be executed after code is pushed to make sure nothing is broken. Tests are usually run from CI to verify this. Continuous delivery is making the build available on GitHub for testers.

## API Design and Implementation

14. **What are REST APIs, and how do they function in your project? Provide an example of a REST endpoint from your user management system.**

15. **What is HATEOAS (Hypermedia as the Engine of Application State)? Provide an example of its implementation in your project's API responses, along with a screenshot.**

## Role-Based Access Control (RBAC)

16. **What is Role-Based Access Control (RBAC) and how is it implemented in your project?**

17. **Explain the different user roles defined in your project (ANONYMOUS, AUTHENTICATED, MANAGER, ADMIN) and their permissions.**

18. **Provide a code example showing how RBAC is enforced in one of your FastAPI endpoints.**

## Route Parameters and Pydantic Schemas

19. **Explain how route parameters are used in FastAPI. Provide an example of a route that takes a parameter and demonstrate how it is used within the endpoint.**

20. **How does FastAPI use Pydantic schemas to generate Swagger documentation? Provide an example from your project where a Pydantic schema is used and show the corresponding Swagger documentation.**

These questions ensure a comprehensive assessment of the students' understanding of the topics related to your project setup, focusing on practical implementations and theoretical concepts.