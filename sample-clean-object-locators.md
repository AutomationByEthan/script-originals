# Production-Ready XPath Locator Library  
**Katalon Studio + Selenium** – 100% XPath, zero brittleness  

> **Philosophy** – Use **semantic attributes** (`aria-label`, `type`, `role`, text) → never rely on class names, indexes, or generated IDs.  
> All locators are **single-line**, **self-documenting**, and **battle-tested** on Chrome / Firefox / Edge.

---

## Core Patterns (copy-paste into Object Repository)

| Element | XPath | Why it’s bullet-proof |
|---------|-------|-----------------------|
| **Account dropdown** | `//button[@aria-label='Settings']` | `aria-label` is added for accessibility – never changes |
| **User Name field** | `//input[@type='email']` | `type` is part of the HTML spec – stable forever |
| **Login button** | `//button[normalize-space()='Log In']` | Exact visible text, ignores whitespace |
| **Password field** | `//input[@type='password']` | Same as email – spec-driven |
| **Submit (primary)** | `//button[@type='submit' and normalize-space()='Save']` | Combines role + text |
| **Close modal** | `//button[@aria-label='Close' or @title='Close']` | Falls back to `title` if needed |


---

## Best Practices Checklist
- [ ] **Never use the copy/paste XPath feature on element inspect** (`/html/body/div[3]/...`)  
- [ ] **Prefer text, labels, roles** over index or generated IDs  
- [ ] **Use `normalize-space()`** to ignore whitespace  
- [ ] **Store in Katalon Object Repository** → reusable across scripts  
- [ ] **Add comments** in Object Repository: `// Purpose: Login button on homepage`


```groovy
// Login
WebUI.setText(findTestObject('Login/fld_Email'), 'admin@kyperian.com')
WebUI.setText(findTestObject('Login/fld_Password'), 'Secret123!')
WebUI.click(findTestObject('Login/btn_Submit'))

// Navigate to Tasks
WebUI.click(findTestObject('Header/btn_AccountDropdown'))  // //button[@aria-label='Settings']
WebUI.click(findTestObject('Sidebar/link_Tasks'))

// Edit first overdue task
WebUI.click(findTestObject('Tasks/btn_Edit_FirstOverdue'))
