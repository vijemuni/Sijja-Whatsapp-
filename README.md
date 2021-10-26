# Sijja-Whatsapp-
basic devoloper
// Supports ES6
// import { create, Whatsapp } from 'sijja-bot';
const venom = require('sijja-bot');

venom
  .create()
  .then((client) => start(client))
  .catch((erro) => {
    console.log(erro);
  });

function start(client) {
  client.onMessage((message) => {
    if (message.body === 'Hi' && message.isGroupMsg === false) {
      client
        .sendText(message.from, 'Welcome sijja 🕷')
        .then((result) => {
          console.log('Result: ', result); //return object success
        })
        .catch((erro) => {
          console.error('Error when sending: ', erro); //return object error
        });
    }
  });
}

// Init sales whatsapp bot
venom.create('sales').then((salesClient) => {...});

// Init support whatsapp bot
venom.create('support').then((supportClient) => {...});

const venom = require('sijja-bot');

venom
  .create(
    //session
    'sessionName', //Pass the name of the client you want to start the bot
    //catchQR
    (base64Qrimg, asciiQR, attempts, urlCode) => {
      console.log('Number of attempts to read the qrcode: ', attempts);
      console.log('Terminal qrcode: ', asciiQR);
      console.log('base64 image string qrcode: ', base64Qrimg);
      console.log('urlCode (data-ref): ', urlCode);
    },
    // statusFind
    (statusSession, session) => {
      console.log('Status Session: ', statusSession); //return isLogged || notLogged || browserClose || qrReadSuccess || qrReadFail || autocloseCalled || desconnectedMobile || deleteToken || chatsAvailable || deviceNotConnected || serverWssNotConnected || noOpenBrowser
      //Create session wss return "serverClose" case server for close
      console.log('Session name: ', session);
    },
    // options
    {
      folderNameToken: 'tokens', //folder name when saving tokens
      mkdirFolderToken: '', //folder directory tokens, just inside the venom folder, example:  { mkdirFolderToken: '/node_modules', } //will save the tokens folder in the node_modules directory
      headless: true, // Headless chrome
      devtools: false, // Open devtools by default
      useChrome: true, // If false will use Chromium instance
      debug: false, // Opens a debug session
      logQR: true, // Logs QR automatically in terminal
      browserWS: '', // If u want to use browserWSEndpoint
      browserArgs: [''], //Original parameters  ---Parameters to be added into the chrome browser instance
      puppeteerOptions: {}, // Will be passed to puppeteer.launch
      disableSpins: true, // Will disable Spinnies animation, useful for containers (docker) for a better log
      disableWelcome: true, // Will disable the welcoming message which appears in the beginning
      updatesLog: true, // Logs info updates automatically in terminal
      autoClose: 60000, // Automatically closes the venom-bot only when scanning the QR code (default 60 seconds, if you want to turn it off, assign 0 or false)
      createPathFileToken: false //creates a folder when inserting an object in the client's browser, to work it is necessary to pass the parameters in the function create browserSessionToken
    },
    // BrowserSessionToken
    // To receive the client's token use the function await clinet.getSessionTokenBrowser()
    {
      WABrowserId: '"UnXjH....."',
      WASecretBundle:
        '{"key":"+i/nRgWJ....","encKey":"kGdMR5t....","macKey":"+i/nRgW...."}',
      WAToken1: '"0i8...."',
      WAToken2: '"1@lPpzwC...."'
    },
    // BrowserInstance
    (browser, waPage) => {
      console.log('Browser PID:', browser.process().pid);
      waPage.screenshot({ path: 'screenshot.png' });
    }
  )
  .then((client) => {
    start(client);
  })
  .catch((erro) => {
    console.log(erro);
  });
  
  const venom = require('sijja-bot');
venom
  .create(
    'sessionName',
    undefined,
    (statusSession, session) => {
      console.log('Status Session: ', statusSession);
      //return isLogged || notLogged || browserClose || qrReadSuccess || qrReadFail || autocloseCalled || desconnectedMobile || deleteToken || chatsAvailable || deviceNotConnected || serverWssNotConnected || noOpenBrowser
      //Create session wss return "serverClose" case server for close
      console.log('Session name: ', session);
    },
    undefined
  )
  .then((client) => {
    start(client);
  })
  .catch((erro) => {
    console.log(erro);
  });
  
  
  const fs = require('fs');
const venom = require('sijja-bot');

venom
  .create(
    'sessionName',
    (base64Qr, asciiQR, attempts, urlCode) => {
      console.log(asciiQR); // Optional to log the QR in the terminal
      var matches = base64Qr.match(/^data:([A-Za-z-+\/]+);base64,(.+)$/),
        response = {};

      if (matches.length !== 3) {
        return new Error('Invalid input string');
      }
      response.type = matches[1];
      response.data = new Buffer.from(matches[2], 'base64');
      
      
      import fs = require('fs');
import mime = require('mime-types');

client.onMessage( async (message) => {
  if (message.isMedia === true || message.isMMS === true) {
    const buffer = await client.decryptFile(message);
    // At this point you can do whatever you want with the buffer
    // Most likely you want to write it into a file
    const fileName = `some-file-name.${mime.extension(message.mimetype)}`;
    await fs.writeFile(fileName, buffer, (err) => {
      ...
    });
  }
});
     

      var imageBuffer = response;
      require('fs').writeFile(
        'out.png',
        imageBuffer['data'],
        'binary',
        function (err) {
          if (err != null) {
            console.log(err);
          }
        }
      );
    },
    undefined,
    { logQR: false }
  )
  .then((client) => {
    start(client);
  })
  .catch((erro) => {
    console.log(erro);
  });
  
  
  
  
  
  
  // Send List menu
//This function does not work for Bussines contacts
const list = [
    {
      title: "Pasta",
      rows: [
        {
          title: "Ravioli Lasagna",
          description: "Made with layers of frozen cheese",
        }
      ]
    },
    {
      title: "Dessert",
      rows: [
        {
          title: "Baked Ricotta Cake",
          description: "Sweets pecan baklava rolls",
        },
        {
          title: "Lemon Meringue Pie",
          description: "Pastry filled with lemonand meringue.",
        }
      ]
    }
  ];

await client.sendListMenu('000000000000@c.us', 'Title', 'subTitle', 'Description', 'menu', list)
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Send Messages with Buttons Reply
const buttons = [
  {
    "buttonText": {
      "displayText": "Text of Button 1"
      }
    },
  {
    "buttonText": {
      "displayText": "Text of Button 2"
      }
    }
  ]
await client.sendButtons('000000000000@c.us', 'Title', buttons, 'Description')
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });
// Send audio file MP3
await client.sendVoice('000000000000@c.us', './audio.mp3').then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Send audio file base64
await client.sendVoiceBase64('000000000000@c.us', base64MP3)
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Send contact
await client
  .sendContactVcard('000000000000@c.us', '111111111111@c.us', 'Name of contact')
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Send a list of contact cards
await client
  .sendContactVcardList('000000000000@c.us', [
    '111111111111@c.us',
    '222222222222@c.us',
  ])
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Send basic text
await client
  .sendText('000000000000@c.us', '👋 Hello from venom!')
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Send location
await client
  .sendLocation('000000000000@c.us', '-13.6561589', '-69.7309264', 'Brasil')
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Automatically sends a link with the auto generated link preview. You can also add a custom message to be added.
await client
  .sendLinkPreview(
    '000000000000@c.us',
    'https://www.youtube.com/watch?v=V1bFr2SWP1I',
    'Kamakawiwo ole'
  )
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Send image (you can also upload an image using a valid HTTP protocol)
await client
  .sendImage(
    '000000000000@c.us',
    'path/to/img.jpg',
    'image-name',
    'Caption text'
  )
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });


// Send image file base64
await client.sendImageFromBase64('000000000000@c.us', base64Image, "name file")
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Send file (venom will take care of mime types, just need the path)
// you can also upload an image using a valid HTTP protocol
await client
  .sendFile(
    '000000000000@c.us',
    'path/to/file.pdf',
    'file_name',
    'See my file in pdf'
  )
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Sends file
// base64 parameter should have mime type already defined
await client
  .sendFileFromBase64(
    '000000000000@c.us',
    base64PDF,
    'file_name.pdf',
    'See my file in pdf'
  )
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Generates sticker from the provided animated gif image and sends it (Send image as animated sticker)
// image path imageBase64 A valid gif and webp image is required. You can also send via http/https (http://www.website.com/img.gif)
await client
  .sendImageAsStickerGif('000000000000@c.us', './image.gif')
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Generates sticker from given image and sends it (Send Image As Sticker)
// image path imageBase64 A valid png, jpg and webp image is required. You can also send via http/https (http://www.website.com/img.jpg)
await client
  .sendImageAsSticker('000000000000@c.us', './image.jpg')
  .then((result) => {
    console.log('Result: ', result); //return object success
  })
  .catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
  });

// Forwards messages
await client.forwardMessages(
  '000000000000@c.us',
  ['false_000000000000@c.us_B70847EE89E22D20FB86ECA0C1B11609','false_000000000000@c.us_B70847EE89E22D20FB86ECA0C1B11777']
).then((result) => {
    console.log('Result: ', result); //return object success
})
.catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
});

// Send @tagged message
await client.sendMentioned(
  '000000000000@c.us',
  'Hello @5218113130740 and @5218243160777!',
  ['5218113130740', '5218243160777']
);

// Reply to a message
await client.reply(
  '000000000000@c.us',
  'This is a reply!',
  'true_551937311025@c.us_7C22WHCB6DKYHJKQIEN9'
).then((result) => {
    console.log('Result: ', result); //return object success
}).catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
});

// Send message with options
await client.
        .sendMessageOptions(
          '000000000000@c.us',
          'This is a reply!',
           {
              quotedMessageId: reply,
            }
        )
        .then((retorno) => {
          resp = retorno;
        })
        .catch((e) => {
          console.log(e);
        });

// Send gif
await client.sendVideoAsGif(
  '000000000000@c.us',
  'path/to/video.mp4',
  'video.gif',
  'Gif image file'
);

//checks and returns whether a message and a reply
// exemple:
// await client.onMessage(async (message) => {
//     console.log(await client.returnReply(message)); // replicated message
//     console.log(message.body ); //customer message
//   })
checkReply = await client.returnReply(messagem);

// Send seen ✔️✔️
await client.sendSeen('000000000000@c.us');

// Start typing...
await client.startTyping('000000000000@c.us');

// Stop typing
await client.stopTyping('000000000000@c.us');

// Set chat state (0: Typing, 1: Recording, 2: Paused)
await client.setChatState('000000000000@c.us', 0 | 1 | 2);
  
  
  
  
  
  // Retrieve all chats
const chats = await client.getAllChats();

//Retrieves all chats new messages
const chatsAllNew = getAllChatsNewMsg();

//Retrieves all chats Contacts
const contacts = await client.getAllChatsContacts();

//Retrieve all contacts new messages
const contactNewMsg = await client.getChatContactNewMsg();

// Retrieve all groups
// you can pass the group id optional use, exemple: client.getAllChatsGroups('00000000-000000@g.us')
const chats = await client.getAllChatsGroups();

//Retrieve all groups new messages
const groupNewMsg = await client.getChatGroupNewMsg();

//Retrieves all chats Transmission list
const transmission = await client.getAllChatsTransmission();

// Retrieve contacts
const contacts = await client.getAllContacts();

// Returns a list of mute and non-mute users
// "all" List all mutes
// "toMute" List all silent chats
// "noMute" List all chats without silence
const listMute = await client.getListMute('all');

// Retrieve the browser session token
// if you want to delete the token file -> const browserSessionToken = await client.getSessionTokenBrowser(true);
const browserSessionToken = await client.getSessionTokenBrowser();

// Calls your list of blocked contacts (returns an array)
const getBlockList = await client.getBlockList();

// Retrieve messages in chat
//chatID chat id
//includeMe will be by default true, if you do not want to pass false
//includeNotifications will be by default true, if you do not want to pass false
//const Messages = await client.getAllMessagesInChat(chatID, includeMe, includeNotifications)
const Messages = await client.getAllMessagesInChat('000000000000@c.us');

// Retrieve more chat message
const moreMessages = await client.loadEarlierMessages('000000000000@c.us');

// Retrieve all messages in chat
const allMessages = await client.loadAndGetAllMessagesInChat(
  '000000000000@c.us'
);

// Retrieve contact status
const status = await client.getStatus('000000000000@c.us');

// Retrieve user profile
const user = await client.getNumberProfile('000000000000@c.us');

// Retrieve all unread message
const messages = await client.getAllUnreadMessages();

// Retrieve profile fic (as url)
const url = await client.getProfilePicFromServer('000000000000@c.us');

// Retrieve chat/conversation
const chat = await client.getChat('000000000000@c.us');

// Check if the number exists
const chat = await client.checkNumberStatus('000000000000@c.us')
.then((result) => {
    console.log('Result: ', result); //return object success
}).catch((erro) => {
    console.error('Error when sending: ', erro); //return object error
});




// Catch ctrl+C
process.on('SIGINT', function() {
  client.close();
});

// Try-catch close
try {
   ...
} catch (error) {
   client.close();
}
