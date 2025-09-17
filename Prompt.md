## Updated Cursor Prompt for Next.js 15 + Tailwind 4

```
I have a Next.js 15 project with Prisma already initialized. Create a minimal task management system with the following specifications:

**Tech Stack (already set up):**
- Next.js 15 with App Router
- TypeScript
- Tailwind CSS 4
- Prisma with PostgreSQL (cloud database)
- JWT authentication
- shadcn/ui components
- bcryptjs for password hashing

**Database Schema (update existing prisma/schema.prisma):**
```

model User {
id String @id @default(cuid())
email String @unique
password String
name String
role Role @default(USER)
tasks Task[]
createdAt DateTime @default(now())
}

model Task {
id String @id @default(cuid())
title String
description String?
status TaskStatus @default(TODO)
deadline DateTime?
assignedTo String
assignedUser User @relation(fields: [assignedTo], references: [id])
createdAt DateTime @default(now())
updatedAt DateTime @updatedAt
}

enum Role {
ADMIN
USER
}

enum TaskStatus {
TODO
IN_PROGRESS
COMPLETED
}

```

**Design Requirements:**
- **Mobile-first responsive design** using Tailwind CSS 4 syntax
- Use shadcn/ui components: Button, Input, Card, Dialog, Select, Table, Badge, Form, Textarea, DatePicker
- Confirmation dialogs for destructive actions (delete tasks)
- Clean, modern UI with proper spacing and typography
- Loading states and error handling with Toast notifications
- Use Tailwind 4's updated class names and features

**Next.js 15 Specific Features:**
- Use React 19 features where applicable
- Leverage Next.js 15's improved App Router
- Use Server Actions for form handling
- Implement proper async/await patterns with React 19
- Use the latest caching and data fetching patterns

**Authentication Flow:**
- JWT stored in httpOnly cookies
- Middleware protection with Next.js 15 middleware patterns
- Auto-redirect: Admin → /admin/tasks, User → /user/tasks

**Pages & Components:**

1. **Login/Register Pages (/login, /register):**
   - shadcn Form components with validation
   - Card layout centered on screen
   - Mobile-optimized form fields using Tailwind 4 classes

2. **Admin Dashboard (/admin/tasks):**
   - **Mobile-first layout:** Use Tailwind 4's container queries and responsive features
   - **Add Task Button:** Prominent FAB-style or full-width on mobile
   - **Task Creation Dialog:** Modal with shadcn Dialog containing:
     - Form with Input (title), Textarea (description), DatePicker (deadline), Select (assign user)
     - Form validation with error states
   - **Task Table/Cards:** Responsive - cards on mobile, table on desktop
   - **Filters Section:** Select dropdowns for Assigned To, Status with clear button
   - **Task Actions:** Edit (inline or modal), Delete with confirmation Dialog
   - **Status Updates:** Select dropdown with color-coded badges

3. **User Dashboard (/user/tasks):**
   - **Simple card layout** optimized for mobile
   - Task cards showing: title, description, deadline, current status
   - **Status update only:** Select dropdown per task
   - Clean, minimal interface

**Key UI/UX Features:**
- **Confirmation Dialogs:** Use shadcn AlertDialog for delete confirmations
- **Toast Notifications:** Success/error feedback for all actions
- **Loading States:** Skeleton loading for tables/cards, button loading states
- **Form Validation:** Real-time validation with error messages
- **Responsive Design:** Use Tailwind 4's improved responsive utilities
- **Touch-friendly:** Adequate touch targets (44px minimum)
- **Status Colors:**
  - TODO: gray badge
  - IN_PROGRESS: blue badge
  - COMPLETED: green badge

**Required shadcn/ui Components to install:**
```

npx shadcn@latest add button input card dialog select table badge form textarea calendar popover alert-dialog toast skeleton

```

**Next.js 15 & React 19 Patterns:**
- Use Server Components by default
- Client Components only when needed (forms, interactivity)
- Server Actions for all form submissions
- Proper async/await in Server Components
- Use React 19's useActionState for form handling
- Implement proper error boundaries

**API Routes (prefer Server Actions):**
- Server Actions for auth operations
- Server Actions for task CRUD
- API routes only when needed for client-side calls

**File Structure:**
```

src/
├── app/
│ ├── login/page.tsx
│ ├── register/page.tsx  
│ ├── admin/tasks/page.tsx
│ ├── user/tasks/page.tsx
│ ├── actions/ (Server Actions)
│ │ ├── auth.ts
│ │ └── tasks.ts
├── components/
│ ├── ui/ (shadcn components)
│ ├── TaskDialog.tsx (Create/Edit modal)
│ ├── TaskCard.tsx (Mobile task display)
│ ├── TaskTable.tsx (Desktop table)
│ ├── DeleteConfirmDialog.tsx
│ ├── TaskFilters.tsx
│ └── StatusBadge.tsx
├── lib/
│ ├── auth.ts
│ ├── db.ts  
│ └── utils.ts
├── middleware.ts

```

**Tailwind 4 Specific Features:**
- Use new container queries: `@container` utilities
- Leverage improved responsive breakpoints
- Use updated color palette and spacing system
- Implement modern CSS Grid and Flexbox utilities
- Use Tailwind 4's enhanced form styling

**Mobile Optimizations:**
- Stack layout on screens < 768px using Tailwind 4's responsive system
- Full-width buttons and forms on mobile
- Touch-friendly interactions with proper spacing
- Collapsible sections using Tailwind 4's animation utilities

**Seed Data:**
Create admin@test.com (password123) and 2 test users with sample tasks.

Build this as a production-ready, mobile-first application leveraging Next.js 15 and Tailwind 4's latest features. Focus on modern React 19 patterns, Server Actions, and excellent mobile UX.
```
