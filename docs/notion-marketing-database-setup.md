# Marketing & Content Database Setup Guide

## Quick Setup Steps

1. **Navigate to Project Management Page**
   - Go to: https://www.notion.so/Project-management-2d79790bc30e80cebdabc42d36bbaf60

2. **Create Database**
   - Click below the existing "Tasks" database
   - Type `/database` and select "Database - Inline"
   - Name it: **Marketing & Content**

3. **Add Properties** (follow order below)

---

## Database Properties Schema

### 1. Title (Auto-created)
- **Property Name**: Title
- **Type**: Title
- **Usage**: Content title or campaign name

### 2. Type
- **Property Type**: Select
- **Options**:
  - 🟣 Campaign (Purple)
  - 🔵 Blog Post (Blue)
  - 🔴 Video (Red)
  - 🟢 Social Post (Green)
  - 🟠 Email Newsletter (Orange)

### 3. Status
- **Property Type**: Select
- **Options** (6-stage workflow):
  - ⚪ Idea (Gray)
  - 🟡 Draft (Yellow)
  - 🟠 Review (Orange)
  - 🔵 Scheduled (Blue)
  - 🟢 Published (Green)
  - 🟤 Archived (Brown)

### 4. Campaign
- **Property Type**: Select
- **Options** (add as needed):
  - 🔵 Q1 2025 Launch (Blue)
  - 🟣 Product Education (Purple)
  - 🩷 Brand Awareness (Pink)
  - 🟢 SEO Content (Green)
  - 🟠 Holiday Campaign (Orange)

### 5. Platform
- **Property Type**: Multi-select
- **Options**:
  - 🔴 YouTube (Red)
  - 🔵 Twitter/X (Blue)
  - 🔵 LinkedIn (Blue)
  - 🩷 Instagram (Pink)
  - 🔵 Facebook (Blue)
  - 🟣 Blog (Purple)
  - ⚪ Website (Gray)
  - 🟠 Email (Orange)

### 6. Priority
- **Property Type**: Select
- **Options**:
  - 🔴 High (Red)
  - 🟡 Medium (Yellow)
  - ⚪ Low (Gray)

### 7. Publish Date
- **Property Type**: Date
- **Usage**: When content goes live

### 8. Assigned To
- **Property Type**: Person
- **Usage**: Content creator/owner

### 9. Tags
- **Property Type**: Multi-select
- **Options**:
  - 🟢 SEO (Green)
  - 🟠 Paid (Orange)
  - 🔵 Organic (Blue)
  - 🟣 Evergreen (Purple)
  - 🔴 Trending (Red)
  - 🩷 Educational (Pink)
  - 🟡 Promotional (Yellow)

### 10. Content URL
- **Property Type**: URL
- **Usage**: Link to published content

### 11. Notes
- **Property Type**: Text
- **Usage**: Description, talking points, content brief

---

## Recommended Views

### View 1: Content Pipeline (Default)
- **Type**: Board
- **Group By**: Status
- **Sort**: Priority (High to Low), then Publish Date
- **Filter**: None
- **Show**: All properties

### View 2: By Campaign
- **Type**: Board
- **Group By**: Campaign
- **Sort**: Publish Date
- **Filter**: Type ≠ Campaign
- **Show**: Type, Status, Platform, Publish Date

### View 3: Publishing Calendar
- **Type**: Calendar
- **Date Property**: Publish Date
- **Filter**: Status = Scheduled OR Status = Published
- **Show**: Type, Platform, Assigned To

### View 4: Active Campaigns
- **Type**: Table
- **Filter**: Type = Campaign AND Status ≠ Archived
- **Sort**: Priority, Publish Date
- **Show**: All properties

---

## Usage Workflow

### Creating a Campaign
1. Create new item, set Type = "Campaign"
2. Fill in Title, Campaign name, Priority
3. Add Notes with campaign objectives
4. Set Status = "Idea"
5. Add associated content pieces (link in Campaign property)

### Creating Content
1. Create new item, select content Type
2. Link to Campaign
3. Select Platform(s)
4. Add Title, Notes/brief
5. Assign To creator
6. Set Priority and target Publish Date
7. Progress through Status stages

### Publishing Workflow
```
Idea → Draft → Review → Scheduled → Published → Archived
  ↓       ↓       ↓         ↓           ↓          ↓
Brainstorm  Write  Edit   Queue    Launch    Cleanup
```

---

## Sample Data Structure

### Example Campaign Entry
```
Title: Q1 Product Launch
Type: Campaign
Status: In Progress
Campaign: Q1 2025 Launch
Priority: High
Publish Date: 2025-03-15
Assigned To: Marketing Team
Tags: Promotional, Paid
Notes: Major product release with multi-channel promotion
```

### Example Content Entry
```
Title: "10 Ways to Boost Productivity with Our App"
Type: Blog Post
Status: Draft
Campaign: Q1 2025 Launch
Platform: Blog, LinkedIn, Twitter
Priority: High
Publish Date: 2025-02-01
Assigned To: Content Writer
Tags: SEO, Organic, Educational
Content URL: (to be added)
Notes: Target keywords: productivity app, workflow optimization
```

---

## Best Practices

1. **Always link content to campaigns** - Makes tracking ROI easier
2. **Update Status regularly** - Keep pipeline visible
3. **Use Tags consistently** - Helps filter and analyze
4. **Set realistic Publish Dates** - Better than missed deadlines
5. **Document in Notes** - Future reference for what worked
6. **Archive old content** - Keep database clean
7. **Review weekly** - Adjust priorities based on performance

---

## Integration Tips

- **Link to Tasks database**: Create relation property to track technical tasks
- **Add Analytics**: Create formula/number properties for views, engagement
- **Budget tracking**: Add number property for campaign spend
- **Performance metrics**: Add properties for conversion rate, ROI
- **Content repository**: Link to design files, drafts in separate database

---

## Next Steps After Setup

1. Create 2-3 sample entries to test workflow
2. Set up the recommended views
3. Customize Campaign options to match your marketing plan
4. Add team members and assign ownership
5. Link to existing Tasks database if needed
6. Consider adding automation (Notion API/Zapier) for status updates

---

*Created: 2025-12-28*
*For: Project Management - Marketing & Content Database*
