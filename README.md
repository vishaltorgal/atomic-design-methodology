# Atomic Design Methodology

***Atomic Design*** is a UI methodology that builds complex interfaces from small, reusable components.

Atomic Design builds UI step by step from small reusable parts to full pages.

<img width="408" height="189" alt="image" src="https://github.com/user-attachments/assets/0f1f882f-2400-4405-8ed1-cbe46d3bb482" />

## Example: Login screen using Atomic Design

1️⃣ Atom – Button
```jsx
// atoms/Button.jsx
export function Button({ children }) {
  return <button>{children}</button>;
}
```
2️⃣ Atom – Input
```jsx
// atoms/Input.jsx
export function Input(props) {
  return <input {...props} />;
}
```
3️⃣ Molecule – FormField (Label + Input)
```jsx
// molecules/FormField.jsx
import { Input } from "../atoms/Input";

export function FormField({ label, ...props }) {
  return (
    <div>
      <label>{label}</label>
      <Input {...props} />
    </div>
  );
}
```
4️⃣ Organism – LoginForm
```jsx
// organisms/LoginForm.jsx
import { FormField } from "../molecules/FormField";
import { Button } from "../atoms/Button";

export function LoginForm() {
  return (
    <form>
      <FormField label="Email" type="email" />
      <FormField label="Password" type="password" />
      <Button>Login</Button>
    </form>
  );
}
```
5️⃣ Template – AuthTemplate
```jsx
// components/templates/AuthTemplate.jsx
export function AuthTemplate({ children }) {
  return (
    <div style={{ maxWidth: "400px", margin: "40px auto" }}>
      <header>
        <h2>Welcome Back</h2>
      </header>

      <main>{children}</main>

      <footer>
        <small>© 2026 Company</small>
      </footer>
    </div>
  );
}
```
6️⃣ Page – LoginPage
```jsx
// components/pages/LoginPage.jsx
import { AuthTemplate } from "../templates/AuthTemplate";
import { LoginForm } from "../organisms/LoginForm";

export function LoginPage() {
  return (
    <AuthTemplate>
      <LoginForm />
    </AuthTemplate>
  );
}
```
***Folder structure***
```jsx
components/
├── atoms/
│   ├── Button.jsx
│   └── Input.jsx
├── molecules/
│   └── FormField.jsx
├── organisms/
│   └── LoginForm.jsx
├── templates/
│   └── AuthTemplate.jsx
└── pages/
    └── LoginPage.jsx
```

***What each layer does***
- ***Atoms*** → smallest UI pieces
- ***Molecules*** → simple atoms combinations
- ***Organisms*** → functional sections
- ***Templates*** → page layout only
- ***Pages*** → real screen with behavior
