Engine Module
=============

Documentation
-------------

The `Engine` class acts as the central backend coordinator for the application. It manages authentication, HTTP and WebSocket communications, user session state, post creation, data retrieval, and social features such as following and unfollowing users. The Engine is designed to provide a unified interface for the frontend to interact with all backend services.

Usage – What Does the Software Do?
----------------------------------

- **Authentication Management**:  
  Handles user login, logout, and session checks using the `AuthManager`.
- **HTTP Requests**:  
  Sends and receives data from the backend using `HttpRequestHandler`, including sign-in, post creation, feed retrieval, user profile fetching, and more.
- **WebSocket Communication**:  
  Manages real-time features via `WebsocketHandler`.
- **Post Creation**:  
  Supports creating text, media, and event posts through a unified interface.
- **Feed and Profile Retrieval**:  
  Fetches paginated feed data and user profile information.
- **Media Download**:  
  Handles downloading of media files from the backend.
- **Social Features**:  
  Implements follow and unfollow functionality for users.
- **Auto-Suggest**:  
  Provides user suggestions for search queries.
- **Subject and Participant Count Retrieval**:  
  Fetches available subjects and event participant counts.

Typical usage flow:
1. The frontend calls methods on the `Engine` to perform authentication, fetch data, or create posts.
2. The `Engine` delegates these requests to the appropriate handler (`AuthManager`, `HttpRequestHandler`, or `WebsocketHandler`).
3. The results are returned to the frontend for UI updates.

Maintenance – How Does the Software Do What It Does?
----------------------------------------------------

**Architecture Overview**::

    +-------------------+
    |    Controller     |
    +---------+---------+
              |
    +---------v---------+
    |      Engine       |
    +---------+---------+
              |
    +---------+---------+-----------------------+
    |         |         |                       |
    |         |         |                       |
    v         v         v                       v
    AuthManager   HttpRequestHandler   WebsocketHandler   (Other modules)

**Key Components**:
- `AuthManager`: Handles authentication logic and user session state.
- `HttpRequestHandler`: Performs all HTTP requests to backend endpoints.
- `WebsocketHandler`: Manages real-time WebSocket connections.

**Data Flow**:
1. **Initialization**:  
   - Engine initializes its handlers and sets up connections.
2. **Authentication**:  
   - `logIn` and `isLoggedIn` delegate to `AuthManager`.
3. **HTTP Requests**:  
   - Methods like `createPost`, `getFeed`, `getUserProfile`, `getSubjects`, and `getParticipantsCount` use `HttpRequestHandler`.
4. **WebSocket**:  
   - Real-time features are managed by `WebsocketHandler`.
5. **Error Handling**:  
   - All network operations use try/catch blocks and print errors for debugging.
6. **State Updates**:  
   - After successful operations (e.g., post creation), the UI is updated via the `Controller`.


Best Practices
--------------

- Use `try/catch` for all network operations and provide meaningful error messages.
- Dispose of resources and close connections when no longer needed.
- Validate all input data before sending to backend.
- Use secure protocols (HTTPS/WSS) for all communications.
- Keep the Engine class focused on orchestration; delegate specifics to handler classes.

Future Improvements
-------------------

- Add retry logic for failed network requests.
- Implement request batching and cancellation.
- Enhance error reporting and logging.
- Add caching for frequently accessed data.
- Support for offline mode and data synchronization.
