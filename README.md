# PS4_Tools
Collection Of Open Source PS4 Tools all in one Library 

Supports Unity

## Getting Started

Add the .DLL to your solution. 
Done Dusted and ready to use

### Class Structure

The class strucutre might change in future releases

    namespace PS4_Tools
    ├── PS4_Tools                                 /*Some Defualt Methods For the Tools*/
    │   ├── AppCommonPath()                       /*Returns Working Directory For Tools*/
    │   ├── DeleteDirectory()                     /*Recursive Deletes Directory*/
    ├── SELF                                      /* Reserved class for SELF/ELF Handeling*/
    │   ├──Self_Header                            /*Self Header Class*/ 
    ├── Media                                     /* PS4 Media Class*/
    │   ├── Atrac9                                /*Atrac9 Class*/
    │   ├──   ├── At9Structure                    /*Atract 9 Structure class*/
    │   ├──   ├── LoadAt9()                       /*Allows users to load an at9 for decoding and returns the wav as a byte array*/
    │   ├──   ├── Load_At9()                      /*Allows user to load an at9 to At9Structure*/
    ├── Image                                     /* PS4 Image Class*/
    |   ├── PNG                                   /*PNG Class*/
    │   ├──   ├── Create_PS4_Compatible_PNG       /*Creates a Complatible PS4 PNG*/
    │   ├── DDS                                   /*DDS Class*/
    │   ├──   ├── SavePNGFromDDS                  /*Saves a PNG from a DDS File*/
    │   ├──   ├── GetStreamFromDDS                /*Gets a Stream from a DDS*/   
    │   ├──   ├── GetBitmapFromDDS                /*Gets a Bitmap from a DDS*/
    │   ├──   ├── GetBytesFromDDS                 /*Gets a byte[] from a DDS*/
    │   ├──   ├── CreateDDSFromBitmap             /*Creates a DDS from a Bitmap*/
    │   └── GIMImages                             /*GIM Image Class*/
    ├── RCO                                       /* PS4 RCO Class*/
    │   ├── DumpRco                               /*Dumps a Rco File*/
    │   ├── ReadRco                               /*Reads a RCO file into a RCOFile Container*/
    ├── SaveData                                  /* PS4 SaveData Reserved Class*/
    │   ├── LoadSaveData                          /*Loads a savedata pfs using a SealedKey*/
    ├── Trophy_File                               /* PS4 Trophy Files Reserved Class*/
    │   ├── Trophy_File                           /*Reads a tropy file from a location on disk*/
    │   ├── Load                                  /*Reads a tropy file from a byte[]*/
    │   ├── ExtractFileToMemory                   /*Extracts a tropy file item to a byte[]*/
    ├── Licensing                                 /* PS4 Licensing Reserved Class*/   
    │   ├── LoadSealedKey                         /*Loads a SealedKey file to Sealedkey Structure*/
    │   ├── ReadRif                               /*Loads a rif file to Rif Structure*/
    │   ├── CreateNewRif                          /*Creates a new Rif File*/    
    │   ├── Read_Act                              /*Reads an act.dat file to Act_Dat structure*/
    ├── PKG                                       /* PS4 PKG Handling Class*/ 
    │   ├── Official                              /*Some Methods for Official PKG Items*/
    │   ├──   ├── ReadAllUnprotectedData          /*Deprecated no longer included inside PS4 Tools*/
    │   ├──   ├── StoreItems                      /*Store Items Object Class (Placeholder)*/
    │   ├──   ├── CheckForUpdate                  /*Returns a Update_Structure Type*/
    │   ├──   ├── Get_All_Store_Items             /*Returns a List<StoreItems> With Download Links and some other infrmation*/
    │   ├── SceneRelated                          /*Some Methods for Scene Related PKG Items*/
    |   ├──   ├── GP4                             /*GP4 File Class*/
    |   ├──   ├──   ├── ReadGP4                   /*Reads a GP4 File Into a Custom Object*/    
    |   ├──   ├──   ├── SaveGP4                   /*Saves a GP4 File From a Custom Object*/
    |   ├──   ├── Create_DLC_FKPG                 /*Creates a PS4 Fake DLC Package*/
    |   ├──   ├── IDS                             /*IDS Reserved Class*/
    |   ├──   ├── PARAM_SFO                       /*Param.SFO Reserved Class*/
    |   ├──   ├──   ├── Get_Param_SFO             /*Reads a Param SFO into a Param.sfo structure*/
    |   ├──   ├── NP_Data                         /*NP_Data Reserved Class*/
    |   ├──   ├── NP_Title                        /*NP_Title Reserved Class*/
    |   ├──   ├── ReadPKG                         /*Reads a PKG File (Powered by maxtron)*/
    |   ├──   ├── Read_PKG                        /*Reads all unprotected data from a pkg (Powered by Leecherman)*/
    |   ├──   ├── Rename_pkg_To_ContentID         /*Renames a PKG File to the Content ID of the SFO*/    
    |   ├──   ├── Rename_pkg_To_Title             /*Renames a PKG File to the Title of the SFO*/
    │   ├── PS2_Classics                          /*Class For Building PS2 Classics*/
    |   ├──   ├── Create_Single_ISO_PKG           /*Creates a Single ISO File PS2 Classic*/    
    |   ├──   ├── Create_Multi_ISO_PKG            /*Creates a Multie ISO File PS2 Classic*/
    │   ├── PSP_HD                                /*Class For Building PSP HD Items*/
    │   ├── PUP                                   /*Class For PUP Tools*/
    |   ├──   ├── Unpack_PUP                      /*Unpacks a PUP Files*/
    |   ├──   ├── Read_Pup                        /*Reads a PUP Files to a PlaystationUpdateFile Holder */
    ├── Tools                                     /* PS4 Tools Tools Class*/ 
    │   ├── Get_PS4_File_Type                     /*Gets the ps4 file type from any file supplied to it returns File_Type Enum*/
    └── (More to come)
    
### Using PS4_Tools

Please see the testers form to see how some of the classes work if not documented here

#### Reading a PKG File (Using Official Toolset) /*Deprecated 2018-11-18*/
```c#

```

#### Reading and Saving a GP4
```c#
 PS4_Tools.PKG.SceneRelated.GP4.Psproject project =   PS4_Tools.PKG.SceneRelated.GP4.ReadGP4(@"C:\Users\3deEchelon\Documents\Sony\Crash Bandcioot Twinsanity.gp4");
            if(project.Fmt != "gp4")
            {
                MessageBox.Show("This is not a valid PS4 Project");
                return;
            }

            //lets validate some pkg item info before saving
            if(project.Volume.Package.Passcode.Length != 32)
            {
                MessageBox.Show("Passcode Lentgh is not valid");
            }

            //to save a gp4 

            PS4_Tools.PKG.SceneRelated.GP4.SaveGP4(@"C:\Users\3deEchelon\Documents\Sony\tempworking.gp4", project);
```

#### Displaying a dds file 
```c#
var item = PS4_Tools.Image.DDS.GetBitmapFromDDS(@"C:\Users\3deEchelon\Desktop\PS4\psp Decrypt\Sc0\icon0.dds");
            pictureBox1.Image = item;
```
#### Creating a dds file (Still in development)
```c#
            Bitmap btimap = new Bitmap(@"C:\Users\3deEchelon\Desktop\PS4\psp Decrypt\Sc0\pic0.png");
            PS4_Tools.Image.DDS.CreateDDSFromBitmap(btimap, @"C:\Users\3deEchelon\Desktop\PS4\psp Decrypt\Sc0\test.dds");
           
            //test if dds is corectly saved
            var item = PS4_Tools.Image.DDS.GetBitmapFromDDS(@"C:\Users\3deEchelon\Desktop\PS4\psp Decrypt\Sc0\test.dds");
            pictureBox1.Image = item;
```
#### Reading a PS4Update File
```c#
                    PS4_Tools.PUP pupfile = new PS4_Tools.PUP();
                    PS4_Tools.PUP.PlaystationUpdateFile pup = pupfile.Read_Pup(openFileDialog1.FileName);
```
#### Dumping a RCO File
```c#
 PS4_Tools.RCO.DumpRco(@"C:\Users\3deEchelon\Desktop\PS4\RCO\Sce.Cdlg.GameCustomData.rco");
```

#### Playing a at9 file 
```c#
            System.Media.SoundPlayer player;
            bool Playing = false;

            if (Playing == false)
            {
                var bytes = PS4_Tools.Media.Atrac9.LoadAt9(@"C:\Users\3deEchelon\Desktop\PS4\AT9\prelude1.at9");
                player = new System.Media.SoundPlayer(new MemoryStream(bytes));
                player.Play();

                button6.Text = "Stop Playing";
                Playing = true;
            }
            else
            {
                player.Stop();

                button6.Text = "Play At9";
                Playing = false;
            }
```

#### Get Game Update Information 
```c#
            var item =PS4_Tools.PKG.Official.CheckForUpdate(textBox1.Text);

            /*TitleID Patch Data Is Avaiavle Here*/

            /*Build some string*/
            string update = label1.Text;
            update += "\n Version : " + item.Tag.Package.Version;
            int ver = Convert.ToInt32(item.Tag.Package.System_ver);
            update += "\n System Version : " + ver.ToString("X");
            update += "\n Remaster : " + item.Tag.Package.Remaster;
            update += "\n Manifest File Number of Pieces : " + item.Tag.Package.Manifest_item.pieces.Count;

            label1.Text = update;
```
#### Get Store Items From a Title ID 
``` c#
    var storeitems = PS4_Tools.PKG.Official.Get_All_Store_Items(textBox1.Text);
```

#### Get Unprotected Data From PKG 
```c#
     PS4_Tools.PKG.SceneRelated.Unprotected_PKG ps4pkg = PS4_Tools.PKG.SceneRelated.Read_PKG(@"C:\Users\3deEchelon\Desktop\PS4\Euro.FISHING.COLLECTORS.EDITION.PS4-DUPLEX\Euro.Fishing.Collectors.Edition.PS4-DUPLEX\duplex-euro.fishing.collectors.ed.ps4\Euro.Fishing.Collectors.Edition.PS4-DUPLEX.pkg");

            /*Lets work with the data shall we*/
            /*Display the PSFO in some type of info format*/
            var item = ps4pkg.Param;
           
            for (int i = 0; i < item.Tables.Count; i++)
            {
                listBox3.Items.Add(item.Tables[i].Name + ":" + item.Tables[i].Value);
            }
            /*Display Image*/
            pictureBox2.Image = ps4pkg.Image;

            var trphy = ps4pkg.Trophy_File;

            for (int i = 0; i < trphy.FileCount; i++)
            {
                listBox4.Items.Add(trphy.trophyItemList[i].Name);
            }
```

## Credits

* [Maxton](https://github.com/maxton) - For The Amazing Work He has done for the scene ! (LibOrbisPKG)
* [GarnetSunset](https://github.com/GarnetSunset) - Playstation Store DLC Indexer
* [stooged](https://github.com/stooged) - PS4 DLC Indexer (C#)
* [cfwprph](https://github.com/cfwprpht) - His help and Vita Rco extractor tool
* [IDC](https://github.com/idc) - His PS4 Pup Extractor and other work he has done
* [Leecherman](https://sites.google.com/site/theleecherman/) - His tools are always a great reference for me and does some great work
* [Thealexbarney](https://github.com/Thealexbarney) - His great research done on atrac9 files and decoding them 

