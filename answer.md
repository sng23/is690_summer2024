# Answer These Questions Here, you can add additional pages to answer questions, just link to them so that I can view these questions and see your answer or the link(s) to your answer.

## FastAPI and Pydantic

1. **What role does Pydantic play in FastAPI, and how does it enhance data validation and settings management?**
* Pydantic provides data validation for our python projects. The most often used class is BaseModel, which is a superclass many of our data classes inherit from.
* These are the files on our project that use some part of the pydantic library. Usually, it is to extend from BaseModel, but also used for validation errors and related.
![Alt text](image.png)


2. **Outline the complete process of handling a user login request in your FastAPI application. Provide a step-by-step explanation with code examples from the project.**
The user is directed to the page with the login.html template. The user enters their credentials which are routed via the `@router.post` login_with_form to the UserService.login_user method, which blocks. That method is user_service.py.login_user which calls another method get_by_email and authenticates the session or not. If successful, ther user is redirecetd to the /dashboard page and their access_token cookie is set.

3. **Explain the service repository pattern and how it is applied in your project. Provide an example of how routes are managed and linked to services.**

## Database Management with Alembic and SQLAlchemy

4. **How does Alembic manage database migrations, and why is this important for maintaining database schemas?**
   - Illustrate with an example of a migration script from the project.

## Pytest

5. **Why is Pytest critical for the development of the API?**

## JWT and User Authentication

6. **Explain the functioning of JWT (JSON Web Tokens) in user authentication. How are JWTs generated, encoded, and used within the project?**
   - [Read this article and link to the code in the user management.](https://supertokens.com/blog/what-is-jwt)
   - Include a code snippet showing how JWTs are implemented in the project.

7. **Decode the following JWT and explain its contents:**
   - Token: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJqb2huLmRvZUBleGFtcGxlLmNvbSIsInJvbGUiOiJBRE1JTiIsInVzZXJfaWQiOiJjZGY4M2QzZi0zNzQ5LTRjZGQtOTRlYS1hNTVjZmMwNDhkMGYiLCJleHAiOjE3MTc2MTY4MjAuMjIwNzA5fQ.ANS8PgUiwPCmOvnZLYTCy_5WzLyhCDOx8aF4xu-Kaz8`
   - Use [jwt.io](https://jwt.io/) to decode and explain the contents.

8. **Describe the user registration logic in your project. Provide a pseudo-code workflow from the registration request to storing the user in the database.**

9. **Detail the steps involved in the user email verification process. Provide a pseudo-code workflow from sending a verification email to activating the user's account.**

## Security Practices

10. **How do you ensure the security of user passwords in your project? Discuss the hashing algorithm used and any additional security measures implemented.**

11. **Explain the difference between hashing and encoding. Provide examples from your project where each is used:**
    - **Hashing:** Example and explanation with code
    - **Encoding:** Example and explanation with code

## Project Management with Docker and CI/CD

12. **Discuss the advantages of using Docker Compose for running your project. How does it help in maintaining a consistent development and deployment environment?**

13. **Describe the role of GitHub Actions in your project's CI/CD pipeline. How do you automate testing and deployment using GitHub Actions?**

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