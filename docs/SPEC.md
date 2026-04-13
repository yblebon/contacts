# Contact Management System Specification

## Project Overview
- **Project Name**: Secure Contact Manager
- **Type**: Single-page static web application
- **Core Functionality**: A contact management system with encrypted local storage, allowing users to add, edit, delete contacts with fields for name, phone, email, address, and notes
- **Target Users**: Individuals who need to manage personal contacts with security

## Technical Architecture

### Encryption Implementation
- **Algorithm**: AES-GCM (256-bit) via Web Crypto API
- **Key Derivation**: PBKDF2 with SHA-256, 100,000 iterations
- **Salt**: Random 16-byte salt generated on first password set
- **Storage**: Encrypted data stored in localStorage
- **IV**: Unique 12-byte IV per encryption operation

### Data Model
```javascript
Contact {
  id: string (UUID)
  name: string
  phone: string
  email: string
  address: string
  notes: string
  createdAt: timestamp
  updatedAt: timestamp
}
```

## Visual Specification

### Layout Structure
- **Container**: Centered card layout, max-width 900px
- **Header**: App title with lock icon
- **Auth Section**: Password input (set/unlock) when no password or locked
- **Main Content**: Contact list with search/filter
- **Contact Form**: Modal for add/edit operations

### Color Palette
- **Primary**: #6366f1 (Indigo)
- **Secondary**: #1e293b (Slate dark)
- **Accent**: #22c55e (Green for success)
- **Background**: #0f172a (Dark slate)
- **Surface**: #1e293b (Card background)
- **Text Primary**: #f1f5f9 (Light gray)
- **Text Secondary**: #94a3b8 (Muted gray)
- **Danger**: #ef4444 (Red for delete)
- **Border**: #334155 (Subtle border)

### Typography
- **Font Family**: "DM Sans", sans-serif
- **Headings**: 600 weight
- **Body**: 400 weight
- **Base Size**: 16px

### Components

#### Password Modal
- Centered overlay modal
- Password input field (type="password")
- Show/hide password toggle
- "Unlock" / "Set Password" button
- Error message display

#### Contact List
- Table layout with columns: Name, Phone, Email, Actions
- Hover effect on rows
- Search bar at top
- Empty state message when no contacts

#### Contact Card/Row
- Displays contact info in compact format
- Edit button (pencil icon)
- Delete button (trash icon)
- Click to expand for full details

#### Contact Form Modal
- Fields: Name (required), Phone, Email, Address, Notes
- Input validation for email format
- Save and Cancel buttons
- Title: "Add Contact" or "Edit Contact"

#### Toolbar
- Add Contact button (+ icon)
- Import button (upload icon)
- Export button (download icon)
- Lock button (lock icon) - to re-lock the app

## Interaction Specification

### Authentication Flow
1. **First-time user**: Prompted to set password
2. **Returning user**: Prompted to unlock with password
3. **Wrong password**: Display error, allow retry
4. **Lock app**: Clear decrypted data from memory, show lock screen

### CRUD Operations
- **Add**: Open modal, fill form, save → encrypt → store → update list
- **Edit**: Click edit → populate modal → save → encrypt → store → update list
- **Delete**: Click delete → confirm dialog → remove → encrypt → store → update list
- **Search**: Filter contacts by name, phone, or email in real-time

### Import/Export
- **Export**: Encrypt current contacts with current password, download as .json file
- **Import**: Upload .json file, prompt for password, decrypt and merge/replace

### Keyboard Shortcuts
- Escape: Close modals
- Enter: Submit forms (when focused)

## Acceptance Criteria

1. ✅ User can set a password on first visit
2. ✅ User must enter password to unlock app on subsequent visits
3. ✅ All contact data is encrypted in localStorage
4. ✅ User can add new contacts with name, phone, email, address, notes
5. ✅ User can edit existing contacts
6. ✅ User can delete contacts with confirmation
6. ✅ User can search/filter contacts
7. ✅ User can export contacts to encrypted JSON file
8. ✅ User can import contacts from encrypted JSON file
9. ✅ App can be locked, requiring password re-entry
10. ✅ Responsive design works on mobile and desktop
11. ✅ All UI elements are styled consistently
12. ✅ Data persists across browser sessions
