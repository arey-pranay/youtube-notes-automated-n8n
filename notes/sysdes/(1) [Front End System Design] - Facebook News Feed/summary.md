# Front-End System Design: Facebook News Feed

## TL;DR
This system design focuses on building a front-end architecture for a Facebook News Feed, addressing key requirements like infinite scroll, user interaction, and data fetching. It breaks down the design into core components, data models, API endpoints, and optimization strategies, emphasizing practical considerations for a large-scale application. The goal is to create a performant and accessible user experience.

## Key Takeaways
- The front-end system design for a news feed involves breaking down the UI into reusable components like Story, Comment List, and Comment Input.
- Data models are crucial for representing information like stories, comments, media, and user details, often using interfaces for structure.
- API endpoints are designed to fetch and manipulate data efficiently, supporting operations like getting posts, creating comments, and subscribing to updates.
- Optimization techniques such as image optimization, code splitting, lazy loading, and caching are essential for a smooth user experience.
- Accessibility is a critical consideration, requiring features like proper ARIA attributes and keyboard navigation.

## Timestamped Sections
- [00:04] **Introduction** — The video begins by introducing the topic of front-end system design, specifically focusing on building a Facebook News Feed.
- [01:13] **General Requirements** — The presenter outlines the fundamental requirements for the news feed, including handling data, components, APIs, and optimization.
- [01:40] **Specific Requirements** — Detailed requirements are discussed, such as infinite scroll, user interaction (likes, comments, shares), and support for various media types.
- [02:10] **Data Models** — The presenter starts defining the data models for stories and comments, including properties like ID, author, media, date, content, and origin.
- [03:50] **Component Architecture** — The core components of the news feed are visualized, including the News Feed itself, Story, StoryCard, Comment List, and Comment Input.
- [10:00] **Data Entities** — The data entities are further elaborated, including details about media types (link, video), user information (ID, nickname), and data origin.
- [15:15] **API Endpoints** — Key API endpoints are identified, such as `getPosts`, `createPost`, `createComment`, and `subscribeNewsStories`, outlining their parameters and purpose.
- [21:13] **Edge Cases** — The discussion shifts to edge cases, including loading new stories, long polling, web sockets, and Server-Sent Events (SSE) for real-time updates.
- [29:58] **Infinite Scroll Design** — The concept of infinite scroll is illustrated with a visual representation of the "active zone" and "intersection zone" for loading stories.
- [33:30] **Optimization Techniques** — Various optimization techniques are presented, including network performance improvements (gzip, webp, brotli, png), rendering performance, JavaScript performance, and image optimization.
- [41:10] **PWA Mode** — The implementation of PWA (Progressive Web App) mode is discussed, focusing on application cache and service workers.
- [45:05] **Accessibility** — Key accessibility considerations are highlighted, such as supporting different color schemas, ARIA live attributes for inputs, and alt attributes for images.
- [46:15] **Hot Keys** — Essential hotkeys for navigating the feed are listed, including actions like creating new stories, posting, scrolling, and accessing help.

## Core Concepts Explained

### Front-End System Design
Front-end system design involves architecting the user interface and client-side logic of a web application. It focuses on how different components interact, how data is fetched and managed, and how to ensure a performant, scalable, and accessible user experience. This includes defining UI components, state management, API interactions, routing, and optimization strategies.

### Component Architecture
Component architecture is a design pattern where an application's UI is broken down into independent, reusable pieces called components. Each component encapsulates its own logic, markup, and styling. This modular approach promotes code reusability, maintainability, and easier testing. Examples in this context include the `Story` component, `CommentList` component, and `CommentInput` component.

### Data Models
Data models define the structure and types of data used within an application. They act as blueprints for how information is organized and accessed. In front-end development, these are often represented using interfaces or classes in languages like TypeScript. For a news feed, data models would include structures for `Story`, `Comment`, `Media`, and `User`, specifying properties like IDs, text content, timestamps, and relationships.

### API Endpoints
API (Application Programming Interface) endpoints are specific URLs or communication channels that allow the front-end to interact with the back-end services. They define the operations that can be performed, such as fetching data (e.g., `getPosts`), creating or modifying data (e.g., `createComment`), or subscribing to real-time updates. Designing efficient and well-defined APIs is crucial for seamless data flow.

### Optimization Techniques
Optimization in front-end development aims to improve the performance and user experience of a web application. Key techniques include:
- **Image Optimization:** Compressing images and using modern formats like WebP or AVIF to reduce file size and improve loading times.
- **Code Splitting:** Breaking down JavaScript bundles into smaller chunks that are loaded on demand, rather than loading the entire application at once.
- **Lazy Loading:** Deferring the loading of non-critical resources (like images or components) until they are needed, improving initial page load performance.
- **Caching:** Storing frequently accessed data or resources locally (e.g., in the browser cache or using service workers) to reduce server requests and speed up subsequent interactions.
- **Gzip/Brotli Compression:** Compressing network requests to reduce bandwidth usage and speed up data transfer.
- **Server-Side Rendering (SSR):** Rendering the initial HTML on the server to improve perceived performance and SEO.
- **Web Workers:** Offloading computationally intensive tasks to background threads to prevent blocking the main UI thread.
- **CSS Class Naming Strategy:** Using a consistent and efficient naming convention for CSS classes (e.g., BEM) to improve maintainability and prevent style conflicts.

### PWA (Progressive Web App) Mode
PWAs are web applications that leverage modern web capabilities to provide an app-like experience to users. Key features include offline access, background synchronization, and the ability to be installed on a user's device. This is achieved through technologies like Service Workers and Application Cache.

### Accessibility
Accessibility in web development ensures that applications can be used by everyone, including people with disabilities. This involves adhering to standards like WCAG (Web Content Accessibility Guidelines) and implementing features such as:
- **Semantic HTML:** Using appropriate HTML tags to convey meaning and structure.
- **ARIA attributes:** Providing additional information to assistive technologies (like screen readers) about UI elements and their states.
- **Keyboard Navigation:** Ensuring all interactive elements are navigable and operable using a keyboard.
- **Color Contrast:** Providing sufficient contrast between text and background colors for readability.
- **Alt Attributes:** Supplying descriptive alternative text for images.

## Interview Perspective
### Why This Matters
Understanding front-end system design is crucial for building performant, scalable, and user-friendly web applications. Interviewers assess your ability to break down complex problems, choose appropriate technologies, and implement solutions that consider various aspects like performance, scalability, and accessibility.

### Concepts Likely to Be Asked
- **Component Architecture:** How would you design a reusable `Story` component? What props would it take? How would you handle its state?
- **Data Fetching:** Explain different strategies for fetching data for an infinite scroll feed (e.g., cursor-based pagination, offset-based pagination). What are the trade-offs?
- **Optimization:** How would you optimize the loading of images and JavaScript? What are the benefits of code splitting and lazy loading?
- **API Design:** Discuss the differences between REST and GraphQL APIs and when you might choose one over the other. How would you design an API for fetching news feed data?
- **State Management:** How would you manage the state of a complex front-end application like a news feed? (e.g., Redux, Context API, Zustand).
- **Accessibility:** What are the key principles of web accessibility, and how would you ensure your application is accessible?

### At a Glance Checkpoints
- [ ] Can you explain the concept of component-based architecture and its benefits?
- [ ] Can you give an example of how you would structure data models for a social media feed?

## Quick Reference
*   **Component-based Architecture:** UI broken into reusable, independent pieces.
*   **Data Models:** Define structure for `Story`, `Comment`, `Media`, `User`.
*   **API Endpoints:** `getPosts`, `createComment`, `subscribeNewsStories`.
*   **Optimization:** Image optimization (WebP), code splitting, lazy loading, caching, Gzip/Brotli, SSR, Web Workers.
*   **PWA:** Service Workers, Application Cache for offline access.
*   **Accessibility:** Semantic HTML, ARIA attributes, keyboard navigation, color contrast, alt text.
*   **Infinite Scroll:** Uses sentinels (top/bottom) and intersection observers to load data as the user scrolls.
*   **API Choices:** REST vs. GraphQL (REST for simple requests, GraphQL for complex data fetching).

**Category:** System Design
**Tags:** `frontend`, `system design`, `react`, `javascript`, `performance`, `optimization`, `accessibility`, `api`, `pwa`, `component architecture`, `data models`
**Interview Relevance:** Must Know
**Difficulty:** Intermediate
**Est. Read Time:** 15 min

## My Notes
FE SD

---

**Source:** https://www.youtube.com/watch?v=5vyKhm2NTfw&list=PLI9W87-Dqn7j_x6QtR6sUjycJR7nQLBqT&index=1&t=5s  
**Saved:** 2026-05-16T08:49:46.137Z
**AI Source:** gemini

<img width="1426" height="619" alt="image" src="https://github.com/user-attachments/assets/f6c0f770-558e-4233-a021-e36dcfa09e72" />
<img width="401" height="257" alt="image" src="https://github.com/user-attachments/assets/8d717e1a-61ef-478c-a1db-2d06f76376d9" />


