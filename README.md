# GridGladiators-React-Java-Tic-Tac-Toe-Tournament

## Description
Create a web-based tic-tac-toe tournament app. The front-end is built with React, and the back-end uses Java with Spring Boot, JPA, H2 and WebSocket for real-time updates.

## Tech Stack
- Java 17+
- Spring Boot (Web, WebSocket, Data JPA)
- H2 Database (in-memory)
- Spring WebSocketHandler
- React (Create React App)
- JavaScript (ES6+)
- WebSocket API

## Requirements
- Provide REST endpoint to create and fetch games (using @RestController and JpaRepository)
- Persist game state transitions in a relational DB (H2 or another JPA datasource)
- Broadcast moves in real time to all clients (Spring WebSocketHandler + JS WebSocket API)
- Build UI to display and update the game board (manage state in React with useState/useEffect)
- Validate win/draw conditions on the server (implement tic-tac-toe logic in a Java service)

## Installation
1. Clone the repository:
   bash
   git clone https://github.com/your-username/GridGladiators-React-Java-Tic-Tac-Toe-Tournament.git
   cd GridGladiators-React-Java-Tic-Tac-Toe-Tournament
   

2. Back-end (Java/Spring Boot):
   - Ensure Java 17+ and Maven are installed.
   - Configure application properties in `backend/src/main/resources/application.properties` if you need a file-based or external DB.

   Start the Spring Boot server:
   bash
   cd backend
   mvn clean spring-boot:run
   

3. Front-end (React):
   - Ensure Node.js (14+) and npm or Yarn are installed.

   Install dependencies and start:
   bash
   cd frontend
   npm install    # or yarn install
   npm start      # or yarn start
   

## Usage
- With both servers running, open http://localhost:3000 in your browser.
- Create a new game or fetch existing games from the lobby.
- Click cells to make moves; the UI updates in real time across all connected clients.
- The server will automatically detect wins or draws and broadcast the final result.

## Implementation Steps
1. Initialize a Spring Boot project with Web, WebSocket, Data JPA and H2 dependencies.
2. Create a `Game` JPA entity and a `GameRepository` extending `JpaRepository<Game, Long>`.
3. Implement a `GameController` with REST endpoints:
   - `POST /api/games` to create a new game
   - `GET /api/games` to list all games
   - `GET /api/games/{id}` to fetch a specific game
4. Build a `GameService` to handle game state transitions and validate win/draw conditions.
5. Configure an in-memory H2 datasource in `application.properties` for persistence.
6. Set up a `WebSocketHandler` and register it under `/ws/moves` to broadcast and receive moves.
7. In React, scaffold the app using Create React App and organize components (Board, Cell, Lobby).
8. Use `useState` and `useEffect` to manage board state and fetch game data via REST.
9. Implement a WebSocket client in React to listen for `/ws/moves` and dispatch state updates on incoming messages.
10. Tie REST and WebSocket layers together: POST moves to `/api/games/{id}/move`, then broadcast via WebSocket.
11. Test game flow: create games, make moves from multiple browser windows, verify real-time sync.

## API Endpoints
- POST  /api/games            → Create a new game
- GET   /api/games            → List all games
- GET   /api/games/{id}       → Get game by ID
- POST  /api/games/{id}/move  → Submit a move (payload: { player: "X"|"O", position: 0–8 })