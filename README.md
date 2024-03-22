# getway-race
“Keno” Documentation by “Code This Lab S.r.l.” v1.0
“Keno”
Created: 09/10/2015
By: Code This Lab S.r.l.
Email: info@codethislab.com

Thank you for purchasing our game. If you have any questions that are beyond the scope of this help file, please feel free to email via user page contact form here. Thanks so much!

Table of Contents
Description
Folder Content
Getting Started
HTML Structure
CSS Files and Structure
Source Code
Game functions
Change Graphic
Disable Sounds
Wordpress Plugin
A) Description - top
Keno is a HTML5 Gambling Game. Enjoy this stylish gambling game!

The ZIP package contains the game with 1920x1080 resolution that scales to fit the whole screen device
Just warning that for very wide screens, the game may not be perfectly full screen. The game is fully compatible with all most common mobile devices.
Sounds are enabled for mobile but we can't grant full audio compatibility on all mobile devices due to some well-know issue between some mobile-browser and HTML5. So if you want to avoid sound loading, please read Disable Sound section).
WARNING: Sounds can't be enabled for Windows Phone as this kind of device have unsolved issues with 'audio' and 'video' tag.

B) Folder Content - top
ctl_arcade_wp_plugin:
This folder contains the zip package that can be used with our Wordpress plugin "CTL Arcade" (http://codecanyon.net/item/ctl-arcade-wordpress-plugin/13856421).
game
This folder contains the full game source code ready to be edited.
live_demo
This folder contains the obfuscated code. You should upload this folder on your server if you don't need to make any changes.
readme
This folder contains the package instructions.
thumbs
This folder contains all game icons.
C)Getting Started - top
To install the game just upload on your server the game folder live_demo.

Game Embedding: The proper way to embed the game is in a full-screen web page or in an iframe.
In the first case the game will fit the screen size, in the second, that of the iframe.
If the iframe size matches that of the screen, the game will fit accordingly.
The alignment will be proportioned to the aspect ratio of the game.
To install the game in a WordPress website, we suggest to use our plugin CTL Arcade .

Save Score: if you need to call your php function for saving score, you can add it in the index.html file:
?
1
2
3
4
5
6
7
8
$(document).ready(function(){
    var oMain = new CMain();
     
    $(oMain).on("save_score", function (evt, iMoney) {
        //alert("iMoney: "+iMoney );
    });
});
Localization: You can easily change game text for different languages, changing string in CLang.js
?
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
                    TEXT_PRELOADER_CONTINUE = "START GAME";
TEXT_GAMEOVER  = "YOU LOST YOUR CREDITS";
TEXT_CURRENCY  = "$";
 
TEXT_MIN       = "-";
TEXT_PLUS      = "+";
 
TEXT_PLAY1     = "PLAY ONE";
TEXT_PLAY5     = "PLAY FIVE";
TEXT_UNDO      = "UNDO";
TEXT_CLEAR     = "CLEAR";
 
TEXT_PAYOUTS   = "PAYOUTS";
TEXT_HITS      = "HITS";
TEXT_PAYS      = "PAYS";
TEXT_CREDITS_DEVELOPED = "DEVELOPED BY";
 
TEXT_CONGRATULATIONS = "Congratulations!";
TEXT_SHARE_1 = "You collected <strong>" ;
TEXT_SHARE_2 = " points</strong>!<br><br>Share your score with your friends!";
TEXT_SHARE_3 = "My score is ";
TEXT_SHARE_4 = " points! Can you do better?";
D)HTML Structure - top
This game have the canvas tag in the body. The ready event into the body calls the main function of the game: CMain().
The head section declares all the javascript functions of the game. The whole project uses a typical object-oriented approach.
In the init function there are 4 mapped events that can be useful eventually for stats

?
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
  <script>
   $(document).ready(function(){
             $(oMain).on("start_session", function(evt) {
                    //THIS EVENT IS TRIGGERED WHEN PLAY BUTTON IN MENU SCREEN IS CLICKED
             });
              
            $(oMain).on("end_session", function(evt) {
                    //THIS EVENT IS TRIGGERED WHEN GAME IS OVER OR THE EXIT BUTTON IS CLICKED.
            });
             
            $(oMain).on("bet_placed", function (evt, oBetInfo) {
                //THIS EVENT IS CALLED WHEN PLAY BUTTON IS CLICKED.
            });
     
            $(oMain).on("save_score", function(evt,iScore) {
                    //THIS EVENT IS TRIGGERED WHEN REELS STOPS AFTER A SPIN. IT CAN BE USEFUL TO CALL PHP SCRIPTS (NOT PROVIDED IN THE PACKAGE) THAT SAVE THE SCORE.
             });
              
             $(oMain).on("show_interlevel_ad", function(evt) {
                    //THIS EVENT IS TRIGGERED EVERY N SPIN. MAY BE USEFUL TO CALL ADS SCRIPT. PLEASE EDIT PARAM 'num_spin_ads_showing' in INDEX.HTML TO SET THIS VALUE.
             });
              
             $(oMain).on("share_event", function(evt,iScore) {
                    //THIS EVENT IS TRIGGERED WHEN USER CLICK EXIT BUTTON. CAN BE USEFUL TO CALL SHARING FEATURE SCRIPTS.
             });
           });
         
  </script>
   
<canvas id="canvas" class="ani_hack" width="1920" height="1080"> </canvas>
Game option: You can easily customize game setting when creating a new instance of the game in index.html file
?
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
var oMain = new CMain({
                        bank_money : 100,
                        start_player_money: 100,
                 
                        win_occurrence : [    
                                            "-",
                                            65, //WIN OCCURRENCE WITH 2 NUMBERS CHOSEN
                                            60, //WIN OCCURRENCE WITH 3 NUMBERS CHOSEN
                                            55, //WIN OCCURRENCE WITH 4 NUMBERS CHOSEN
                                            50, //WIN OCCURRENCE WITH 5 NUMBERS CHOSEN
                                            45, //WIN OCCURRENCE WITH 6 NUMBERS CHOSEN
                                            40, //WIN OCCURRENCE WITH 7 NUMBERS CHOSEN
                                            35, //WIN OCCURRENCE WITH 8 NUMBERS CHOSEN
                                            30, //WIN OCCURRENCE WITH 9 NUMBERS CHOSEN
                                            25  //WIN OCCURRENCE WITH 10 NUMBERS CHOSEN
                                        ],
                                         
                         
                        //PAYOUT VALUES TABLE: {#HITS, BET MULTIPLY, HITS OCCURRENCE}
                        payouts : [                
                                    {hits: ["-"],           pays: ["-"],                            occurrence: [0]},                   //PAYOUTS FOR 1 NUMBERS
                                    {hits: [2,1],           pays: [9,1],                            occurrence: [20,80]},               //PAYOUTS FOR 2 NUMBERS
                                    {hits: [3,2],           pays: [47,2],                           occurrence: [20,80]},               //PAYOUTS FOR 3 NUMBERS
                                    {hits: [4,3,2],         pays: [91,5,2],                         occurrence: [10,30,60]},            //PAYOUTS FOR 4 NUMBERS
                                    {hits: [5,4,3],         pays: [820,12,3],                       occurrence: [10,30,60]},            //PAYOUTS FOR 5 NUMBERS
                                    {hits: [6,5,4,3],       pays: [1600,70,4,3],                    occurrence: [10,20,30,40]},         //PAYOUTS FOR 6 NUMBERS
                                    {hits: [7,6,5,4,3],     pays: [7000,400,21,2,1],                occurrence: [5,10,20,30,35]},       //PAYOUTS FOR 7 NUMBERS
                                    {hits: [8,7,6,5,4],     pays: [10000,1650,100,12,2],            occurrence: [5,10,20,30,35]},       //PAYOUTS FOR 8 NUMBERS
                                    {hits: [9,8,7,6,5,4],   pays: [10000,4700,335,44,6,1],          occurrence: [1,4,10,20,30,35]},     //PAYOUTS FOR 9 NUMBERS
                                    {hits: [10,9,8,7,6,5],  pays: [10000,4500,1000,142,24,5],       occurrence: [1,4,10,15,30,40]}      //PAYOUTS FOR 10 NUMBERS
 
                                ],
                                 
                                 
                        animation_speed : 300,
                        audio_enable_on_startup:false, //ENABLE/DISABLE AUDIO WHEN GAME STARTS 
                        fullscreen:true, //SET THIS TO FALSE IF YOU DON'T WANT TO SHOW FULLSCREEN BUTTON
                        check_orientation:true,     //SET TO FALSE IF YOU DON'T WANT TO SHOW ORIENTATION ALERT ON MOBILE DEVICES
                        show_credits:true,           //SET THIS VALUE TO FALSE IF YOU DON'T TO SHOW CREDITS BUTTON
                        //////////////////////////////////////////////////////////////////////////////////////////
                        ad_show_counter: 5     //NUMBER OF TURNS PLAYED BEFORE AD SHOWN
                        //
                        //// THIS FUNCTIONALITY IS ACTIVATED ONLY WITH CTL ARCADE PLUGIN.///////////////////////////
                        /////////////////// YOU CAN GET IT AT: /////////////////////////////////////////////////////////
                        // http://codecanyon.net/item/ctl-arcade-wordpress-plugin/13856421?s_phrase=&s_rank=27 ///////////
                       });
E) CSS Files and Structure - top
The game use two CSS files. The first one is a generic reset file. Many browser interpret the default behavior of html elements differently. By using a general reset CSS file, we can work round this. Keep in mind, that these values might be overridden somewhere else in the file.

The second file contains all of the specific stylings for the canvas and some hack to be fully compatible with all most popular mobile devices

F) Source Code - top
This game contains:

jQuery
Our custom scripts
CreateJs plugin
jQuery is a Javascript library that greatly reduces the amount of code that you must write.
The game have the following js files:
CMain: the main class called by the index file.
This file controls the sprite_lib.js file that manages the sprite loading, the loop game and initialize the canvas with the CreateJs library
ctl_utils: this file manages the canvas resize and its centering
sprite_lib: this class loads all images declared in the main class
settings: general game settings
CLang: global string variables for language localization
CPreloader: simple text preloader to show resources loading progress
CMenu: simple menu with the play button
CGfxButton: this class create a standard button
CToggle: this class create a standard toggle button
CTextButton: this class create a standard text button
CGame: this class manages the game logic
CInterface: this class controls game GUI that contains text and buttons
CAnimBalls: this class manages the ball movement when numbers are extracted
CNumToggle: this class manages the number button from 1 to 80.
CEndPanel: this class manages the panel that is shown when the game is over
CPayouts: this class manages the panel that shows all payouts
CDisplayPanel: this class manages the panels that shows some info
CreateJs is a suite of modular libraries and tools which work together to enable rich interactive content on open web technologies via HTML5.
Resuming, the complete game flow is the following:

The index.html file calls the CMain.js file after ready event is called
The main class calls CPreloader.js to init preloader text and start sprite loading
When all sprites contained in "/sprites" and "/sounds" folder are loaded, the main class removes the preloader and calls the CMenu.js file that shows the main menu
If the user click the Play button in main menu, the CGame.js class is called and game starts
If the user click on the exit button in the up-right corner, the game returns to the menu screen
G) Game functions - top
In this section will be explained all the most important functions used in CGame.js file.

_init()
This function attach on the canvas some game sprites like background (oBg)and the GUI.
_initCells()
This function init grid with all clickable numbers.
_onButNumRelease()
This function is called when user click a number.
play()
This function is called when number must be extracted.
_checkWin
This function check if player wins or not.
_extractWinCombination
This function get 20 numbers with a winning payout.
_extractLosingCombination()
This function get 20 losing numbers.
_checkContinueGame()
This function checks if user has enough money to continue playing.
H) Change Graphic - top
You can easily change all the game graphic, replacing all the file you need in the "/sprites" folder. Just respect file format (.png or .jpg) and size if you don't want to change any code line.
I) Disable Sounds - top
If you want to disable all the sounds for mobile devices, you have to change the following value in settings.js file:

?
1
var DISABLE_SOUND_MOBILE = true;


J) Wordpress Plugin - top
CTL Arcade will allow you to add a real arcade on your worpress website, in this way your users will be more involved and will stay connected longer.

It's possible to add Ads banner at the beginning of each game and at the end of each level. This will give you a new tool to increase your revenues.

Your own users will promote your website sharing their scores on the main Social Networks, with no extra costs for you.

You'll get by default the score-sharing on Twitter. To add Facebook just follow the guideline below.

3 widgets can be added in your pages through a shortcode.
Game iframe
Rate the Game
Leaderboard
Minimum Requirements:

PHP 4.3
WordPress 4.3.1
HTML5
Canvas
Javascript / jQuery
This plugin is designed to work only with games built by Code This Lab.

You can find it here!
ctl arcade

Once again, thank you so much for purchasing this game. Feel free to contact us if you have any questions or issue relating to this game. No guarantees, but we'll do our best to assist.

CODE THIS LAB S.R.L.

Go To Table of Contents

