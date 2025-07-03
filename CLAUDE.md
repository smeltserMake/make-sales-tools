# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a bookmarklet-based sales tool hub that provides drag-and-drop automation tools for the Make.com sales team. The project centers around a single HTML file that serves as a micro-site where sales team members can drag bookmarklets to their bookmark bar for instant access to sales automation tools.

## Architecture

**Core Components:**
- `salesforce-bookmarklet.html` - Main micro-site serving draggable bookmarklet tools with professional UI
- Embedded JavaScript bookmarklet code that extracts Salesforce Opportunity IDs and sends data to webhook endpoints
- AWS API Gateway integration for CSP compliance and security
- Responsive design with modern UI/UX following Make.com design principles

**Data Flow:**
1. User drags bookmarklet from website to bookmark bar
2. When clicked on Salesforce Opportunity pages, bookmarklet extracts ID using regex: `/\/lightning\/r\/Opportunity\/([a-zA-Z0-9]{15,18})\/view/`
3. Sends JSON payload to AWS API Gateway endpoint: `https://54jsznj7h4.execute-api.us-east-2.amazonaws.com/prod/webhook`
4. AWS Lambda processes request and forwards to Make.com webhook
5. Response displayed in styled popup overlay for 30 seconds with auto-close
6. Payload format: `{opportunityId, sourceUrl, timestamp}`

## Development Commands

**Local Development:**
```bash
# Serve locally for testing
python3 -m http.server 8000
# or
npx serve .

# Test bookmarklet in browser
# Open salesforce-bookmarklet.html
# Drag bookmarklet to bookmark bar
# Navigate to Salesforce opportunity page
# Click bookmarklet to test functionality
```

**Deployment:**
```bash
# Deploy to static hosting (GitHub Pages, Netlify, Vercel)
# No build process required - pure HTML/CSS/JS
```

## Key Features

**Bookmarklet Functionality:**
- Automatic Opportunity ID extraction from Salesforce Lightning URLs
- AWS API Gateway proxy for CSP compliance
- Formatted JSON response display in popup overlay
- Error handling with user-friendly alerts
- Cross-browser compatibility (Chrome, Firefox, Safari, Edge)

**UI/UX Design:**
- Drag-and-drop interface for easy bookmark creation
- Hover tooltips explaining each tool's purpose
- Technical details section with expandable content
- Professional design matching Make.com aesthetics
- Mobile-responsive layout

**Security Features:**
- AWS API Gateway acts as secure proxy
- HTTPS encryption for all requests
- No client-side API key storage required
- Compliant with Salesforce Content Security Policy
- Server-side credential management in AWS Lambda

## File Structure

```
salesforce-bookmarklet.html     # Main micro-site with embedded bookmarklet
├── Embedded CSS               # Styling for professional UI
├── Embedded JavaScript        # Bookmarklet code and site functionality
└── Technical documentation    # Expandable details section
```

## Bookmarklet Code Structure

The main bookmarklet performs these operations:
1. **URL Pattern Matching** - Detects Salesforce Opportunity pages
2. **Data Extraction** - Extracts Opportunity ID from URL
3. **Payload Construction** - Creates JSON with ID, URL, timestamp
4. **HTTP Request** - POST to AWS API Gateway endpoint
5. **Response Handling** - Displays formatted response in popup
6. **Error Management** - Shows user-friendly error messages

## AWS Integration

**Architecture Flow:**
```
Salesforce → Bookmarklet → AWS API Gateway → AWS Lambda → Make.com Webhook
```

**Benefits:**
- Bypasses Salesforce CSP restrictions
- Centralizes API key management
- Provides request logging and monitoring
- Enables response transformation
- Maintains security best practices

## Usage Instructions

**For End Users:**
1. Visit the micro-site
2. Drag the "🎯 MSP Generator" tool to bookmark bar
3. Navigate to any Salesforce Opportunity page
4. Click the bookmark to trigger automation
5. View response in popup window

**For Developers:**
- Update bookmarklet code in the `bookmarkletCode` variable
- Modify AWS endpoint URL as needed
- Customize popup styling and behavior
- Add new tools to the tools grid section

## Browser Compatibility

- **Chrome**: Full support
- **Firefox**: Full support  
- **Safari**: Full support
- **Edge**: Full support
- **Mobile browsers**: Limited (bookmarklet functionality varies)

## Security Considerations

- Uses AWS API Gateway for secure request routing
- No sensitive credentials exposed in client-side code
- HTTPS encryption for all communications
- Compliant with corporate IT security policies
- No installation or permissions required

## Future Enhancements

**Planned Features:**
- Demo scenario runner bookmarklet
- Additional automation tools
- Response data copying functionality
- Enhanced error handling and retry logic
- Usage analytics and tracking

## Deployment

The micro-site can be hosted on any static hosting service:
- GitHub Pages
- Netlify
- Vercel
- AWS S3 + CloudFront
- Any web server

No build process or dependencies required - pure HTML/CSS/JavaScript.