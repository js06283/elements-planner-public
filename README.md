# Elements Festival Planner

A modern, interactive festival planning application that allows groups to track which shows they want to attend at the Elements Festival. The application loads the real Elements Festival schedule from a CSV file and supports real-time collaboration using Firebase.

## 🚀 Quick Setup Checklist

1. **Clone this repository**
2. **Set up Firebase** (optional - for real-time features)
3. **Add your group members** to `index.html` (dropdown menu)
4. **Add colors for your group** to `script.js` (personColors object)
5. **Deploy to Vercel** (optional - for sharing with your group)

## Features

- **Real Elements Festival Schedule**: Loads the actual Elements Festival lineup from CSV data
- **Interactive Show Selection**: Click on shows to add/remove yourself from the attendee list
- **Real-time Updates**: See changes instantly across all users (with Firebase)
- **Multi-day Support**: Plan across Friday, Saturday, and Sunday
- **Multiple Stages**: Track shows across Water, Air, Earth, and Fire stages
- **Modern UI**: Beautiful, responsive design with smooth animations
- **Data Persistence**: Save your plans locally or in the cloud
- **Export/Import**: Backup and restore your festival plans
- **Comments System**: Add comments to shows for group coordination

## Quick Start

1. **Clone the repository**:

   ```bash
   git clone <your-repo-url>
   cd elements-festival-planner
   ```

2. **Set up Firebase** (optional but recommended for real-time features):

   - Follow the [Firebase Setup](#firebase-setup) instructions below

3. **Customize your group**:

   - Edit `index.html` to add your group members to the dropdown
   - Edit `script.js` to add colors for your group members

4. **Run locally**:

   ```bash
   # Using Python
   python -m http.server 8000

   # Using Node.js
   npx serve .
   ```

5. **Access the application**:

   - Open `http://localhost:8000` in your browser

## Firebase Setup

### 1. Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" and follow the setup wizard
3. Give your project a name (e.g., "elements-festival-planner")
4. Choose whether to enable Google Analytics (optional)

### 2. Enable Firestore Database

1. In your Firebase project, go to "Firestore Database"
2. Click "Create database"
3. Choose "Start in test mode" for development (you can secure it later)
4. Select a location close to your users

### 3. Get Your Configuration

1. In your Firebase project, go to "Project settings" (gear icon)
2. Scroll down to "Your apps" section
3. Click "Add app" and select "Web" (</>)
4. Register your app with a nickname
5. Copy the configuration object

### 4. Update the Configuration

1. Open `firebase-config.js`
2. Replace the `firebaseConfig` object with your actual configuration:

```javascript
const firebaseConfig = {
	apiKey: "your-actual-api-key",
	authDomain: "your-project-id.firebaseapp.com",
	projectId: "your-project-id",
	storageBucket: "your-project-id.appspot.com",
	messagingSenderId: "your-messaging-sender-id",
	appId: "your-app-id",
	measurementId: "your-measurement-id",
};
```

### 5. Set up Security Rules (Optional but Recommended)

1. In Firestore Database, go to "Rules" tab
2. Replace the default rules with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true; // Allow all access for now
    }
  }
}
```

## Vercel Deployment

### 1. Install Vercel CLI

```bash
npm install -g vercel
```

### 2. Deploy to Vercel

1. **Login to Vercel**:

   ```bash
   vercel login
   ```

2. **Deploy the project**:

   ```bash
   vercel
   ```

3. **Follow the prompts**:

   - Link to existing project or create new
   - Set project name
   - Confirm deployment settings

4. **Set up environment variables** (if needed):
   - Go to your Vercel dashboard
   - Select your project
   - Go to Settings > Environment Variables
   - Add any required environment variables

### 3. Custom Domain (Optional)

1. In your Vercel dashboard, go to your project
2. Click "Settings" > "Domains"
3. Add your custom domain
4. Follow the DNS configuration instructions

## Customizing Your Group

### Adding Group Members to Dropdown

1. Open `index.html`
2. Find the `nameSelect` dropdown (around line 24)
3. Add your group members:

```html
<select id="nameSelect" class="name-select">
	<option value="">Select a name...</option>
	<option value="John">John</option>
	<option value="Jane">Jane</option>
	<option value="Bob">Bob</option>
	<option value="Alice">Alice</option>
	<option value="custom">Other (enter custom name)</option>
</select>
```

### Adding Colors for Group Members

1. Open `script.js`
2. Find the `personColors` object (around line 15)
3. Add colors for your group members:

```javascript
this.personColors = {
	John: "#FF6B6B", // Coral Red
	Jane: "#4ECDC4", // Turquoise
	Bob: "#45B7D1", // Sky Blue
	Alice: "#96CEB4", // Mint Green
	Other: "#F7DC6F", // Golden Yellow for custom names
};
```

## CSV Format

The application automatically loads the real Elements Festival schedule from `Elements_Festival_Full_Schedule__All_Days_.csv`. This includes:

- **3 Days**: Friday, Saturday, Sunday
- **4 Stages**: Water, Air, Earth, Fire
- **Real Artists**: All actual performers from the Elements Festival lineup
- **Accurate Times**: Exact show times as scheduled

### CSV Structure

The CSV file has the following structure:

```csv
Day,Time,Stage,Artist
Friday,3:30PM-4:20PM,Earth,MACHETE
Friday,4:30PM-5:30PM,Earth,MADDY O'NEAL
Friday,6:00PM-7:30PM,Earth,PAPADOSIO
Saturday,3:30PM-4:45PM,Earth,SPLINTERED SUNLIGHT
Sunday,2:30PM-3:30PM,Earth,VINCENT ANTONE
```

### Required Columns:

- **Day**: Day of the festival (e.g., "Friday", "Saturday", "Sunday")
- **Time**: Show time (e.g., "3:30PM-4:20PM", "2:30PM-3:30PM")
- **Stage**: Stage name (e.g., "Water", "Air", "Earth", "Fire")
- **Artist**: Artist/act name

### Tips:

- Use consistent day names (e.g., always "Friday" not "Fri")
- Use consistent time format (e.g., "3:00PM" not "3 PM" or "15:00")
- Use consistent stage names (e.g., always "Water" not "Water Stage")

## File Structure

```
elements-festival-planner/
├── index.html                                    # Main HTML structure
├── styles.css                                    # Modern CSS styling
├── script.js                                     # Interactive JavaScript functionality
├── firebase-config.js                           # Firebase configuration and service
├── csv-parser.js                                # CSV parsing utility
├── load-schedule.js                             # Schedule loading functionality
├── Elements_Festival_Full_Schedule__All_Days_.csv # Real Elements Festival schedule
├── vercel.json                                  # Vercel deployment configuration
├── package.json                                 # Project metadata
└── README.md                                    # This file
```

## Usage

1. **Enter Your Name**: Select your name from the dropdown or enter a custom name
2. **Select Shows**: Click on any show to add yourself to the attendee list
3. **Remove Yourself**: Click on a show again or click the "×" next to your name to remove yourself
4. **Real-time Updates**: If using Firebase, see changes from other users in real-time
5. **Export Data**: Use Ctrl/Cmd + E to export your festival plan as JSON
6. **Save Data**: Use Ctrl/Cmd + S to manually save your data
7. **Add Comments**: Click the comment icon on any show to add notes

## Browser Support

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

## Troubleshooting

### Firebase Issues

1. **Connection Failed**: Check your Firebase configuration in `firebase-config.js`
2. **Permission Denied**: Update Firestore security rules (see Firebase Setup)
3. **Domain Not Authorized**: Add your domain to Firebase project settings

### CSV Loading Issues

1. **File Not Found**: Ensure the CSV file is in the correct location
2. **Format Error**: Check that your CSV follows the required format
3. **Encoding Issues**: Save the CSV file as UTF-8

### Deployment Issues

1. **Vercel Build Failed**: Check that all files are committed
2. **Domain Issues**: Verify DNS settings for custom domains
3. **Environment Variables**: Ensure all required variables are set in Vercel

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

If you encounter any issues:

1. Check the browser console for error messages
2. Ensure Firebase is properly configured (if using cloud features)
3. Verify your internet connection (for real-time features)
4. Try clearing your browser's local storage if data seems corrupted
5. Check that the CSV file is accessible and properly formatted

## Future Enhancements

- [ ] User authentication and profiles
- [ ] Show recommendations based on preferences
- [ ] Schedule conflicts detection
- [ ] Social features (sharing plans with friends)
- [ ] Mobile app version
- [ ] Advanced filtering and search
- [ ] Integration with festival APIs
- [ ] Custom schedule import/export
- [ ] Artist information and bios
- [ ] Stage maps and locations
