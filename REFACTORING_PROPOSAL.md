# Documentation Refactoring Proposal

## 1. Chat Widget File Refactoring

### Current State
- **File**: `fern/docs/pages/apps/surfaces/chat.mdx`
- **Size**: 1,223 lines
- **Issues**: Single monolithic file covering installation, configuration, multiple handoff providers, authentication, and programmatic control

### Proposed Structure

Break `chat.mdx` into a main overview page with separate pages for major sections:

```
apps/surfaces/chat/
  ├── index.mdx (Overview + Quick Start)
  ├── installation.mdx
  ├── configuration.mdx (Basic + Advanced Settings)
  ├── live-agent-handoff/
  │   ├── index.mdx (Overview of handoff providers)
  │   ├── salesforce-legacy.mdx
  │   ├── salesforce-messaging.mdx
  │   ├── zendesk.mdx
  │   ├── front.mdx
  │   ├── hubspot.mdx
  │   └── genesys.mdx
  ├── authentication.mdx
  └── programmatic-control.mdx (API methods, event listeners, pushing messages)
```

### Benefits
- **Maintainability**: Each provider's configuration is isolated
- **Discoverability**: Easier to find specific handoff provider docs
- **Performance**: Smaller pages load faster
- **Clarity**: Clear separation of concerns

### Implementation Approach

1. **Main chat page** (`chat/index.mdx`):
   - Overview of chat widget
   - Quick installation snippet
   - Links to detailed sections
   - Basic configuration overview

2. **Separate handoff provider pages**:
   - Each provider gets its own page with complete setup instructions
   - Common patterns (like agent availability) can be referenced
   - Easier to update individual provider docs

3. **Configuration page**:
   - All settings tables and options
   - Widget customization options
   - Metadata passing examples

---

## 2. Tab-Based Information Architecture

### Proposed Top-Level Tabs

#### Tab 1: **Agent Designer**
**Purpose**: Configuration and management of Maven agents

**Contains**:
1. Insights
2. Ask Maven
3. Inbox
4. Conversations
   - Overview
   - Reviewing Conversations
5. Feedback
6. Training Maven
   - Building Knowledge Base
   - Personas
   - Workflows
   - Actions
   - Triggers
   - Evaluating and Improving Maven Quality
7. Simulator (Playground)
8. Settings

**Rationale**: All content related to designing, training, testing, and managing agents within the Agent Designer interface. This includes analytics, knowledge management, testing tools, and configuration.

---

#### Tab 2: **Maven Surfaces**
**Purpose**: Maven's native customer-facing interfaces where users interact with Maven

**Contains**:
- Chat Widget (with sub-pages for handoff, auth, etc.)
- Search
- Instant Answers

**Rationale**: These are Maven's own surfaces where end users interact with the platform. These are built and maintained by Maven.

---

#### Tab 3: **Third-Party Surfaces**
**Purpose**: Integration with external platforms where users can interact with Maven

**Contains**:
- Slack
- Microsoft Teams
- SMS

**Rationale**: These are surfaces that integrate Maven into third-party platforms, allowing users to interact with Maven through their existing communication tools.

---

#### Tab 4: **Ticketing**
**Purpose**: Integrations with ticketing and CRM systems for live agent handoff and ticket management

**Contains**:
- Zendesk
- Salesforce
- HubSpot
- Freshdesk
- Front
- Intercom
- Kustomer
- Zoho
- SharePoint
- Actions
  - OAuth Sign-In Action

**Rationale**: These are backend integrations with ticketing systems and CRMs that enable live agent handoff, ticket creation, and workflow automation.

---

#### Tab 5: **Platform**
**Purpose**: Platform administration and developer resources

**Contains**:
- Security and Privacy Details
- API Overview
- Developer Platform Documentation

**Rationale**: Platform-level administration, security, and developer resources for building custom integrations and applications.

---

#### Tab 6: **Reference**
**Purpose**: Quick reference materials and definitions

**Contains**:
- Glossary
- API Reference (if separate from API Overview)

**Rationale**: Supporting documentation that users reference but don't need in primary workflows.

---

### Visual Structure

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  [Agent Designer] [Maven Surfaces] [Third-Party Surfaces] [Ticketing] [Platform] [Reference]  │
└──────────────────────────────────────────────────────────────────────────────┘
│                                                                                │
│  Content Area (with sidebar navigation within each tab)                        │
│                                                                                │
└──────────────────────────────────────────────────────────────────────────────┘
```

### Migration Mapping

| Current Sidebar Section | New Tab | Notes |
|------------------------|---------|-------|
| Welcome | (Removed or moved to Getting Started) | May be integrated into Agent Designer intro |
| Apps > Surfaces > Chat | Maven Surfaces | Maven's native chat widget |
| Apps > Surfaces > Search | Maven Surfaces | Maven's native search |
| Apps > Surfaces > Instant Answers | Maven Surfaces | Maven's native instant answers |
| Apps > Surfaces > Slack | Third-Party Surfaces | External platform integration |
| Apps > Surfaces > MS Teams | Third-Party Surfaces | External platform integration |
| Apps > Surfaces > SMS | Third-Party Surfaces | External platform integration |
| Apps > Ticketing | Ticketing | All ticketing system integrations |
| Apps > Actions | Ticketing | Actions related to ticketing workflows |
| Train | Agent Designer > Training Maven | Agent training and configuration |
| Preparing Knowledge | Agent Designer > Training Maven | Knowledge setup (part of training) |
| Settings | Agent Designer | Agent settings |
| Conversations | Agent Designer | Operational feature within Agent Designer |
| Inbox | Agent Designer | Knowledge quality management |
| Insights | Agent Designer | Analytics within Agent Designer |
| Feedback | Agent Designer | Feedback management |
| Ask Maven | Agent Designer | Analytics tool within Agent Designer |
| Playground/Simulator | Agent Designer > Simulator | Testing tool |
| Security and Privacy | Platform | Platform admin |
| API Overview | Platform | Developer docs |
| Glossary | Reference | Reference material |
| Language Overview | (May be removed or integrated) | May be part of Training Maven |
| User Roles/Permissions | (May be removed or integrated) | May be part of Settings |

---

## 3. Complete Content Inventory by Tab

### Tab 1: **Agent Designer**

#### Insights
- `insights/overview.mdx`

#### Ask Maven
- `ask-maven/overview.mdx`

#### Inbox
- `inbox.mdx`

#### Conversations
- `conversations/overview.mdx`
- `conversations/reviewing-conversations.mdx`

#### Feedback
- `feedback/overview.mdx`

#### Training Maven
- `train/building-knowledge-base.mdx`
- `train/personas.mdx`
- `train/workflows.mdx`
- `train/actions.mdx`
- `train/triggers.mdx`
- `train/evaluating-and-improving-maven-quality.mdx`
- `preparing-knowledge.mdx` (integrated into Training Maven section)

#### Simulator
- `playground/overview.mdx` (titled "Maven Simulator")

#### Settings
- `settings/overview.mdx`
- `user-roles-and-permissions-in-maven.mdx` (may be integrated into Settings)
- `manage-users-and-permissions.mdx` (may be integrated into Settings)
- `language-overview.mdx` (may be integrated into Settings or Training Maven)

---

### Tab 2: **Maven Surfaces**

#### Chat Widget
- `apps/surfaces/chat.mdx` (to be refactored into multiple pages)
  - Main overview
  - Installation
  - Configuration
  - Live Agent Handoff (with sub-pages for each provider)
  - Authentication
  - Programmatic Control

#### Search
- `apps/surfaces/search.mdx`

#### Instant Answers
- `apps/surfaces/instant-answers.mdx`

---

### Tab 3: **Third-Party Surfaces**

#### Slack
- `apps/surfaces/slack.mdx`

#### Microsoft Teams
- `apps/surfaces/ms-teams.mdx`

#### SMS
- `apps/surfaces/sms.mdx`

---

### Tab 4: **Ticketing**

#### Ticketing Integrations
- `apps/ticketing/zendesk.mdx`
- `apps/ticketing/salesforce.mdx`
- `apps/ticketing/hubspot.mdx`
- `apps/ticketing/freshdesk.mdx`
- `apps/ticketing/front.mdx`
- `apps/ticketing/intercom.mdx`
- `apps/ticketing/kustomer.mdx`
- `apps/ticketing/zoho.mdx`
- `apps/ticketing/sharepoint.mdx`
- `apps/ticketing/HubSpot Documentation.mdx` (may need consolidation with hubspot.mdx)

#### Actions
- `apps/actions/oauth-sign-in-action.mdx`

#### Overview
- `apps/overview.mdx` (may be split or moved to Ticketing tab intro)

---

### Tab 5: **Platform**

#### Security and Privacy
- `security-and-privacy-details.mdx`

#### API Overview
- `api-overview.mdx`

#### Developer Platform Documentation
- (Content from `api-overview.mdx` may be expanded or split into multiple pages)

---

### Tab 6: **Reference**

#### Glossary
- `glossary.mdx`

#### API Reference
- (May be separate from API Overview, or linked from Platform tab)

---

### Unassigned / To Be Determined

#### Welcome
- `welcome.mdx`
  - **Options**: 
    - Could become a landing page before tabs
    - Could be integrated into Agent Designer as an intro/getting started section
    - Could be removed if redundant

### Summary Table: All Content by Tab

| Tab | Section | Files | Count |
|-----|---------|-------|-------|
| **Agent Designer** | Insights | `insights/overview.mdx` | 1 |
| | Ask Maven | `ask-maven/overview.mdx` | 1 |
| | Inbox | `inbox.mdx` | 1 |
| | Conversations | `conversations/overview.mdx`, `conversations/reviewing-conversations.mdx` | 2 |
| | Feedback | `feedback/overview.mdx` | 1 |
| | Training Maven | `train/*.mdx` (6 files), `preparing-knowledge.mdx` | 7 |
| | Simulator | `playground/overview.mdx` | 1 |
| | Settings | `settings/overview.mdx`, `user-roles-and-permissions-in-maven.mdx`, `manage-users-and-permissions.mdx`, `language-overview.mdx` | 4 |
| **Maven Surfaces** | Chat Widget | `apps/surfaces/chat.mdx` (to be refactored) | 1+ |
| | Search | `apps/surfaces/search.mdx` | 1 |
| | Instant Answers | `apps/surfaces/instant-answers.mdx` | 1 |
| **Third-Party Surfaces** | Slack | `apps/surfaces/slack.mdx` | 1 |
| | Microsoft Teams | `apps/surfaces/ms-teams.mdx` | 1 |
| | SMS | `apps/surfaces/sms.mdx` | 1 |
| **Ticketing** | Integrations | `apps/ticketing/*.mdx` (10 files) | 10 |
| | Actions | `apps/actions/oauth-sign-in-action.mdx` | 1 |
| | Overview | `apps/overview.mdx` | 1 |
| **Platform** | Security | `security-and-privacy-details.mdx` | 1 |
| | API | `api-overview.mdx` | 1 |
| **Reference** | Glossary | `glossary.mdx` | 1 |
| **Unassigned** | Welcome | `welcome.mdx` | 1 |

**Total Files**: ~35+ files (not counting chat widget sub-pages after refactoring)

---

## 4. Implementation Recommendations

### Phase 1: Refactor Chat Widget
1. Create new directory structure for chat
2. Split handoff providers into separate files
3. Create index page with navigation
4. Update all internal links

### Phase 2: Implement Tab Structure
1. Update docs configuration to support tabs
2. Reorganize pages into tab-based structure
3. Update navigation components
4. Add breadcrumbs if needed

### Phase 3: Content Updates
1. Add cross-references between related pages
2. Update "Next Steps" sections to reflect new structure
3. Ensure all internal links work
4. Add tab navigation hints in content

---

## 5. Benefits of This Architecture

### For Users
- **Clearer mental model**: Tabs group related functionality
- **Faster navigation**: Less scrolling through long pages
- **Better discoverability**: Related content is grouped together
- **Reduced cognitive load**: Smaller, focused pages

### For Maintainers
- **Easier updates**: Changes to one provider don't affect others
- **Better organization**: Clear separation of concerns
- **Scalability**: Easy to add new providers or features
- **Reduced merge conflicts**: Multiple people can work on different sections

---

## 6. Example: Chat Widget Refactored Structure

### `chat/index.mdx` (Main Overview)
```mdx
---
title: Chat Widget
---

## Overview
Maven offers a chat widget that allows you to embed a Maven experience directly into your website.

## Quick Start

<Steps>
  <Step title="Install the app">
    [Installation steps]
  </Step>
  <Step title="Add to your website">
    [Integration code]
  </Step>
</Steps>

## Configuration

- [Basic Settings](/apps/surfaces/chat/configuration#basic)
- [Advanced Settings](/apps/surfaces/chat/configuration#advanced)
- [Widget Customization](/apps/surfaces/chat/configuration#widget)

## Live Agent Handoff

Connect your chat widget to live agent support:
- [Salesforce (Legacy)](/apps/surfaces/chat/live-agent-handoff/salesforce-legacy)
- [Salesforce Messaging](/apps/surfaces/chat/live-agent-handoff/salesforce-messaging)
- [Zendesk](/apps/surfaces/chat/live-agent-handoff/zendesk)
- [Front](/apps/surfaces/chat/live-agent-handoff/front)
- [HubSpot](/apps/surfaces/chat/live-agent-handoff/hubspot)
- [Genesys](/apps/surfaces/chat/live-agent-handoff/genesys)

## Additional Features

- [Authentication](/apps/surfaces/chat/authentication)
- [Programmatic Control](/apps/surfaces/chat/programmatic-control)
```

### `chat/live-agent-handoff/zendesk.mdx` (Example Provider Page)
```mdx
---
title: Zendesk Live Agent Handoff
---

## Overview
Maven Chat integrates with Zendesk Conversations to provide human support capabilities.

## Requirements
- Zendesk account with Professional plan or above
- Access to the Conversations API
- Admin access to configure integrations

## Setup Process
[Full setup steps from current file]

## Configuration
[Configuration object and options]

## Related
- [Live Agent Handoff Overview](/apps/surfaces/chat/live-agent-handoff)
- [Other Providers](/apps/surfaces/chat/live-agent-handoff)
```

---

## 7. Next Steps

1. **Review and approve** this architecture proposal
2. **Prioritize** which sections to refactor first
3. **Create** new file structure
4. **Migrate** content with proper linking
5. **Test** navigation and user experience
6. **Update** search and indexing if needed

