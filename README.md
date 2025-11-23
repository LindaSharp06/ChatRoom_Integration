# Chat Component: the simplest way to add chat to your React app

<br /><img src="https://github.com/YusukeM317/ChatRoom_ERC721_ERC1155_Integration/blob/main/img/chat interface.png" width="860" />

## About this Chat Component

This Chat Component allows you to build a functioning chat room super quickly.
Sounds simple and is easy to build your app with.
Uses XMPP chat protocol and ejabberd chat server to provide your users with a seamless instant messaging experience.

Once you need more functionality however you will be pleasantly surprised. Our platform behind the chat component offers a plethora of functionalities around chat/social, user profiles, digital wallets, business documents exchange, digital collectables, web3 and AI bots. The history behind Chat Component is following. First, we have built a low-code “super app” engine which we used to drastically speed up app development for our clients. Afterwards, we have open-sourced it for the benefit of other developers. Later on, we realized that whilst developers love what we can do, many of them don’t need such a complex engine with all bells and whistles but a steep learning curver. In most cases you’re after a certain functionality (like a simple chat room) and you need it quick.

Enter this Chat Component which allows you to quickly implement your chat room experience!

Note: scroll below for use cases and functionality break down of this Chat Component.


## Skills used

![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=flat&logo=javascript&logoColor=%23F7DF1E)
![React](https://img.shields.io/badge/react-%2320232a.svg?style=flat&logo=react&logoColor=%2361DAFB) ![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=flat&logno=typescript&logoColor=white) ![JWT](https://img.shields.io/badge/JWT-black?style=flat&logo=JSON%20web%20tokens)


## How to build your chat room on the spot

1. npm create vite@latest
2. specify a name for your project (e.g. "vite-project")
3. select framework and variant (for example, React -> Typescript but may be different depending on your project requirements, it will work with plain Javascript too)

<img src="https://github.com/YusukeM317/ChatRoom_ERC721_ERC1155_Integration/blob/main/img/readme01.png" width="500" />

<img src="https://github.com/YusukeM317/ChatRoom_ERC721_ERC1155_Integration/blob/main/img/readme02.png" width="500" />

4. cd vite-project _(use your name instead of "vite-project")_
5. npm i
6. npm i @ethora/chat-component
7. go to file src/App.tsx and replace it with the below code

```
import { Chat } from "@ethora/chat-component";
import "./App.css";

function App() {
 return (
   <Chat />
 );
}

export default App;
```

7. run like this

```
npm run dev
```

you should see something like this:
<br /><img src="https://github.com/YusukeM317/ChatRoom_ERC721_ERC1155_Integration/blob/main/img/readme03.png" width="350" />

9. Open http://localhost:5173/ in your browser

Voilà - your chat app should work like so:

<img src="https://github.com/YusukeM317/ChatRoom_ERC721_ERC1155_Integration/blob/main/img/readme_animation.gif" width="860" />

ℹ️ Note: User and Chat credentials are hard-coded and login screen is bypassed. This is done so that you can scaffold and test the functionality quickly.
Leave this as is if you only need to demo or validate the chat functionality as part of your project.
If you need to have your own private chats, be able to login multiple users etc then go to https://www.ethora.com/, sign up in the top right which gives you a free account with Ethora backend where you can create your own App, manage your Users and Chats, view stats etc. Copy App ID & App Secret to your chat component code which will then switch to your own App context on the server side. The free tier is generous but should you need extra you can later build your own backend, upgrade to a paid tier from Ethora or use a self-hosted AWS marketplace image from Ethora.

## Extra options (styling etc)

To create custom chat room styles in **App.tsx**:

replace

```
<Chat />
```

with:

```
<Chat
    config={{
    disableHeader: true,
    disableMedia: true,
    colors: { primary: "#4287f5", secondary: "#42f5e9" },
    defaultLogin=true
    googleLogin: {
      firebaseConfig: config, //Ethora app config
      enabled: true,
    },
    }}
    MainComponentStyles={{
      width: "100%",
      height: "500px",
      borderRadius: "16px",
      border: "1px solid #42f5e9",
    }}
    roomJID=""
    user={{ email: "", password: "" }}
      disableHeader?: boolean;

    disableRooms: boolean;
    defaultLogin: boolean;
    disableInteractions: boolean; //disable interactions
    chatHeaderBurgerMenu: boolean; // disable burger menu in room header
    roomListStyles: React.CSSProperties; // used to change room List styles (left)
    chatRoomStyles: React.CSSProperties; // used to change room styles (right)
    setRoomJidInPath: boolean; // used to set RoomId to url
  />
```

ℹ️ Note: Add room and user which are registered at Ethora. After these changes - the pre-written user & room will be changed to yours.

ℹ️ Note:
There is also a prop CustomMessageComponent: React.ComponentType<MessageProps>
This prop is used to fully change styles of messageBubble.
You can find an example here: https://github.com/YusukeM317/ChatRoom_ERC721_ERC1155_Integration/blob/main/src/components/ExampleComponents/CustomMessage.tsx

For styling you can alter **App.css**:

```
#root {
 width: 100%;
 margin: 0 auto;
 text-align: center;
}
```

and **index.css**:

```
body {
 margin: 0;
 display: flex;
 place-items: center;
 min-width: 320px;
 min-height: 100vh;
 width: 100%;
}
```

After these changes you can modify **MainComponentStyles** for your chat.


## Use cases and functionalities details

### LOGIN FUNCTIONALITY

Chat component includes an optional Login / Sign-on screen that allows you to login existing users or sign up new users.
In cases where chat component is embedded into your existing web or app experience, you would likely want to disable and bypass the login screen.

Supported out of the box:

- **Login bypass** (user credentials are passed from your existing backend) ✅
- **E-mail + password** ✅
- **Google SSO** ✅


### CHAT FUNCTIONALITY

#### "One room at a time - chat session"

- Use Case 1: **One global chat room for all users** ✅ - (e.g. chat lobby for all of your website / app users). Simply create a chat room manually and hardcode the UUID into your chat component code.
- Use Case 2: **One chat room per case** ✅ - (e.g. customer support session, AI bot, a chat room for each location or department, web page specific chat etc). You have to create rooms as required by your business logic via Ethora API and then pass the corresponding chat UUID into chat component. Your end User will see the corresponding room.

#### "Multiple rooms - messenger / social app”

- Use Case 3: **Users can switch between Chats** ✅
  Similar to Use Case 2, but also allows your User to switch to the **List of Chats** where they can see chat rooms, the count of new messages and a last message for -each room etc. Users can create new Chats and invite others into Chats (depending on your App settings). This functionality is available in full Ethora app but is currently "work in progress" for Chat Component.

#### Misc core chat functionalities

- **Chat header** ✅ - Header with chat title and Users counter (this is optional and you can disable the header)
- **Message bubbles** ✅ - Message bubbles next to user avatars with message content and timestamp
- **Chat history caching and scrolling** ✅
- **Chat history date divider** ✅
- **Now typing** ✅ - when someone is typing, other room Users will see indication of who is typing

#### Message interactions

- **Message menu** ✅ - Long tap or right click opens message menu with "Reply", "Copy", "Edit", "Delete", "Report" options available as well as send Coin / Item options
- **Emoji Reactions** ✅ - Users are able to long tap / click on the message and send Emoji reactions to the message. Reactions are displayed in the corner of the message bubble.

#### Avatars (profile photos)

- **Basic avatars** ✅ - in chat screen, users can see basic avatars next to chat bubbles. Simply default avatar icon for everyone.
- **"Initials" avatars** ✅ - in Chat scree, users who don't have photos uploaded will show as "initials" avatars generated by taking the first letter of User's first name and last name
- **Google SSO avatars** 🚧 when using Google SSO, their Google profile photo will be automatically displayed as chat avatar
- **Custom profile photos** ✅ - users are able to upload their custom photos when managing their Profile and the mini-photo will be displayed as a chat avatar

#### Notifications

- **Browser and mobile push notifications**  push notifications are useful to alert the User about new messages or transactions related to them when they are not actively using your app / chat in the browser.

### FILE ATTACHMENTS

- **File attachments** ✅ - file attachments, previews, media attachments, audio/video player etc currently are work in progress for chat component

