This is a good coverage of interfaces. I’ll clean it up, correct a small mistake, and add a few **important real-world additions** that many developers overlook (index signatures, interface with classes, function interface, etc.).

Here is a polished and complete version with added clarity and examples:

---

## **Interface in TypeScript**

Interfaces describe the shape of an object. They are used for **type checking**, not for runtime behavior.

```ts
interface NewUser {
  readonly _id: number;           // cannot be modified once assigned
  email: string;
  userId: number;
  googleId?: string;              // optional property
  startTrial: () => string;       // method returning string
  getCoupon(couponName: string): number;  // method with param + return type
}
```

### **Using the Interface**

```ts
const Mohan: NewUser = {
  email: "a@g.com",
  userId: 123,
  _id: 123,
  googleId: "an@gm.com",
  startTrial: () => "Trial Started",
  getCoupon: (name) => {
    return 10;
  }
};
```

### **Important Correction**

Your second object was missing `getCoupon`, and `gitHubToken` didn’t exist yet when you declared it.

```ts
const Mohan1: NewUser = {
  email: "a@g.com",
  userId: 123,
  _id: 123,
  googleId: "an@gm.com",
  startTrial: () => "Trial Started",
  getCoupon: () => 10,
  gitHubToken: "a.aadw.dad"
};
```

---

## **Re-opening / Merging Interfaces**

Interfaces can be **extended later**, even from different files.

```ts
interface NewUser {
  gitHubToken: string;
}

// Now NewUser has: _id, email, userId, googleId, startTrial, getCoupon, gitHubToken
```

This is something **type aliases cannot do**.

---

## **Extending an Interface**

```ts
interface Admin extends NewUser {
  role: "Admin" | "TA" | "Learner";
}
```

---

## **Interface vs Type Alias**

| Feature                            | Interface | Type Alias        |
| ---------------------------------- | --------- | ----------------- |
| Can be reopened/merged             | ✅ Yes     | ❌ No              |
| Can extend other interfaces        | ✅ Yes     | ✅ Yes (using `&`) |
| Used for functions and objects     | ✅ Yes     | ✅ Yes             |
| Used for union, primitives, tuples | ❌ No      | ✅ Yes             |

### **Example: Extending**

**Interface extending interface**

```ts
interface Animal {
  name: string;
}
interface Bear extends Animal {
  honey: boolean;
}
```

**Type using intersection**

```ts
type Animal = {
  name: string;
};
type Bear = Animal & {
  honey: boolean;
};
```

### **Interface Merging**

```ts
interface Window {
  title: string;
}

interface Window {
  ts: any;
}

// ✅ Works: merged together
```

### **Type Cannot Be Reopened**

```ts
type Window = {
  title: string;
};

type Window = {       // ❌ Error
  ts: any;
};
```

---

## **Additional Useful Additions**

### **1. Function Interface**

```ts
interface LoginFn {
  (email: string, password: string): boolean;
}

const login: LoginFn = (email, password) => true;
```

### **2. Interface for Classes**

```ts
interface TakePhoto {
  cameraMode: string;
  filter: string;
  burst: number;
}

class Instagram implements TakePhoto {
  constructor(
    public cameraMode: string,
    public filter: string,
    public burst: number
  ) {}
}
```

### **3. Index Signatures (for dynamic object keys)**

```ts
interface UserDictionary {
  [id: string]: string;
}

const users: UserDictionary = {
  "1": "Mohan",
  "2": "Anwar"
};
```

---

## **Summary**

| Concept    | Key Point                                             |
| ---------- | ----------------------------------------------------- |
| Interface  | Defines object shape; mergeable; extendable           |
| Type Alias | Defines any type; cannot merge; supports unions       |
| Tuple      | Fixed-length typed array                              |
| Enum       | Named constant values; `const enum` is most efficient |

---

If you want, I can now **convert all your TS notes into a single PDF cheat sheet** ready to revise before interviews.
Just say: **Make PDF** 📄✨
