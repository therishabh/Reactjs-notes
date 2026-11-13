# **Component Composition in React**

**Component Composition** is a React concept where we build complex UI by combining smaller, reusable components together.

In simple English:

Instead of creating one big component that handles everything, we create multiple small components and combine them to build the final UI.

Think of it like building a house:

- Bricks are small individual components.
- Walls are made using multiple bricks.
- Rooms are made using multiple walls.
- The complete house is made using multiple rooms.

Similarly, in React, we combine small components to create complex UI.

## **1. Without Component Composition**

Let's say you want to create a user profile card.

You might write everything inside one component:

```
function UserProfile() {
  return (
    <div className="profile-card">
      <img src="/user.png" alt="User" />
      <h2>John Doe</h2>
      <p>Frontend Developer</p>
      <button>Follow</button>
    </div>
  );
}

export default UserProfile;
```

This works perfectly fine.

But imagine your application has:

- User Profile Card
- Product Card
- Dashboard Card
- Notification Card

If you keep writing everything inside large components, your code can become difficult to maintain and reuse.

## **2. With Component Composition**

Now let's break the UI into smaller components.

**Step 1: Create separate components**

```
function UserImage() {
  return <img src="/user.png" alt="User" />;
}

function UserInfo() {
  return (
    <div>
      <h2>John Doe</h2>
      <p>Frontend Developer</p>
    </div>
  );
}

function FollowButton() {
  return <button>Follow</button>;
}
```

**Step 2: Combine these components**

```
function UserProfile() {
  return (
    <div className="profile-card">
      <UserImage />
      <UserInfo />
      <FollowButton />
    </div>
  );
}

export default UserProfile;
```

Here, `UserProfile` combines three smaller components.

This is Component Composition

We are composing smaller components to create a bigger component.

## **3. Composition using the&#x20;**`children`**&#x20;prop**

This is one of the most important concepts in React composition.

React provides a special prop called `children`.

It allows a component to receive and render whatever content is placed between its opening and closing tags.

Let's understand with an example.

**Step 1: Create a reusable Card component**

```
function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}
```

Notice `{children}`.

It represents the content passed inside the Card component.

**Step 2: Use the Card component**

```
function App() {
  return (
    <Card>
      <h2>Welcome!</h2>
      <p>This is my dashboard.</p>
      <button>Explore</button>
    </Card>
  );
}
```

**What happens here?**

React passes everything inside the Card tags as the `children` prop.

The Card component renders that content wherever `{children}` is placed.

### **Why is this useful?**

Because now the same Card component can be used with different content.

```
function App() {
  return (
    <>
      <Card>
        <h2>User Profile</h2>
        <p>John Doe</p>
      </Card>

      <Card>
        <h2>Product Details</h2>
        <p>iPhone 17</p>
      </Card>

      <Card>
        <h2>Notifications</h2>
        <p>You have 3 new messages.</p>
      </Card>
    </>
  );
}
```

One Card component, multiple use cases!

You don't need to create separate Card components for every situation.

## **4. Composition using props**

Composition is not limited to `children`. We can also compose components by passing other components or JSX through props.

Example:

```
function Layout({ header, sidebar, content }) {
  return (
    <div>
      <header>{header}</header>

      <div className="layout">
        <aside>{sidebar}</aside>
        <main>{content}</main>
      </div>
    </div>
  );
}
```

Using it:

```
function App() {
  return (
    <Layout
      header={<h1>My Dashboard</h1>}
      sidebar={<p>Dashboard | Settings</p>}
      content={<h2>Welcome John!</h2>}
    />
  );
}
```

Here:

- `header` receives header JSX.
- `sidebar` receives sidebar JSX.
- `content` receives main content JSX.

This is also component composition.

## **5. Real-world example: Dashboard**

Let's combine everything we learned.

```

function Card({ title, children }) {
  return (
    <div className="card">
      <h2>{title}</h2>
      {children}
    </div>
  );
}

function UserProfile() {
  return (
    <Card title="User Profile">
      <p>Name: John Doe</p>
      <p>Role: Frontend Developer</p>
      <button>View Profile</button>
    </Card>
  );
}

function Statistics() {
  return (
    <Card title="Statistics">
      <p>Total Users: 1200</p>
      <p>Active Users: 950</p>
    </Card>
  );
}

function Dashboard() {
  return (
    <div>
      <h1>Dashboard</h1>

      <UserProfile />
      <Statistics />
    </div>
  );
}

export default Dashboard;

```

Here is the component structure:

**Dashboard**

**UserProfile**

Uses Card

**Statistics**

Uses Card

**Reusable Card Component**

Receives different content through children.

Notice that:

1. Dashboard combines UserProfile and Statistics.
2. UserProfile and Statistics both use Card.
3. Card provides a common structure.
4. Each component controls its own content.

This makes the application modular and easier to maintain.

## **6. Component Composition vs Component Inheritance**

This is an important React interview question.

| Component Composition                 | Component Inheritance                      |
| ------------------------------------- | ------------------------------------------ |
| Combines smaller components together. | Extends one component from another.        |
| Uses props and children.              | Uses class inheritance.                    |
| Recommended approach in React.        | Not commonly used for sharing UI behavior. |
| Flexible and reusable.                | Can create tight coupling.                 |

React recommends composition over inheritance for reusing component behavior and structure.

## **7. Benefits of Component Composition**

| Benefit                | Explanation                                          |
| ---------------------- | ---------------------------------------------------- |
| Reusability            | Use the same component in multiple places.           |
| Maintainability        | Smaller components are easier to update.             |
| Flexibility            | Pass different content to the same component.        |
| Separation of concerns | Each component has a clear responsibility.           |
| Scalability            | Easier to build complex applications.                |
| Testability            | Smaller components are easier to test independently. |

## **8. Interview Questions**

**Q1. What is Component Composition in React?**

Component composition is a technique of combining smaller, reusable components to build larger and more complex UI components. It helps improve code reusability, maintainability and flexibility.

**Q2. How does React support component composition?**

React supports composition mainly through:

- `children` prop.
- Passing JSX as props.
- Nesting components inside other components.

**Q3. What is the children prop?**

`children` is a special React prop that contains the content passed between a component's opening and closing tags.

**Q4. What is the difference between props and children?**

- Props are used to pass data or configuration from parent to child.
- Children is a special prop used to pass nested content inside a component.

**Q5. Why does React recommend composition over inheritance?**

Composition provides more flexibility because components can be combined in different ways without creating tight dependencies between them.



**My recommendation:** As an experienced React developer, focus especially on `children`, passing JSX through props, reusable layouts, and composition patterns. These are frequently useful when designing scalable component architecture in real-world applications.
