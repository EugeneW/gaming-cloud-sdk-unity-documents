# Fresvii Gaming Cloud SDK for Unity

----------
##  Introduction
Fresvii Gaming Cloud SDK for Unity is an integrated backend gaming service for Unity.
With Fresvii, you can easily incorporate various backend services refined to mobile games into your apps for free.

##  Classes
|Namespace|Class|Description|
|-------|------|-----|
|Fresvii.GamingCloud|[FGC](#FGCClass)|Fresvii Gaming Cloud API core function class|
|Fresvii.GamingCloud.Models|[User](#UserClass)|User model class|
|Fresvii.GamingCloud.Models|[SnsAccount](#SnsAccount)|SnsAccount model class|
|Fresvii.GamingCloud.Models|[Thread](#Thread)|Thread model class|
|Fresvii.GamingCloud.Models|[Comment](#Comment)|Comment model class|

## <a name ="FGCClass">FGC Class</a>

Fresvii Gaming Cloud API core function class. The SDK uses static methods of the FGC class.

### Methods

|Name|Description|
|------|-----|
|[FGC.SignUp](#FGC.SignUp)| Sign up a user associated with the app. |
|[FGC.LogIn](#FGC.LogIn)| Returns a session token necessary for the user created with SignUp to perform an operation. |
|[FGC.LogOut](#FGC.LogOut)| Log out. |
|[FGC.GetSnsAccountList](#FGC.GetSnsAccountList)| Gets the list of SNS authentication information registered for the user. |
|[FGC.SetSnsAccount](#FGC.SetSnsAccount)| Save the uie, identifies users in the SNS, acquired through SNS authentication and SNS service name associating with signed in user. |
|[FGC.DeleteSnsAccount](#FGC.DeleteSnsAccount)| Delete the SNS authentication information specified by the id. |
|[FGC.GetAccount](#FGC.GetAccount)| Get the signed in users status. |
|[FGC.PatchAccount](#FGC.PatchAccount)| Change the signed in users status. |
|[FGC.GetUser](#FGC.GetUser)| Get the users status specified by id. |
|[FGC.GetUserList](#FGC.GetUserList)| Get the user list specified by conditions. |
|[FGC.RegisterRemoteNotification](#FGC.RegisterRemoteNotification)| Register a notification. |
|[FGC.UnregisterRemoteNotification](#FGC.UnregisterRemoteNotification)| Unregister a notification. |
|[FGC.GetForumThreads](#FGC.GetForumThreads)| Get the forum thread list. |
|[FGC.CreateThread](#FGC.CreateThread)| Create a new thread. |
|[FGC.DeleteThread](#FGC.DeleteThread)| Delete a thread. |
|[FGC.GetThreadComments](#FGC.GetThreadComments)| Get the thread comment list. |
|[FGC.Subscribe](#FGC.Subscribe)| Subscribe to a thread. |
|[FGC.Unsubscribe](#FGC.Unsubscribe)| Unsubscribe from a thread. |
|[FGC.AddComment](#FGC.AddComment)| Add a new comment to a thread. |
|[FGC.EditComment](#FGC.EditComment)| Edit a comment. |
|[FGC.DeleteComment](#FGC.DeleteComment)| Delete a comment. |
|[FGC.LikeComment](#FGC.LikeComment)| Like a comment. |
|[FGC.UnlikeComment](#FGC.UnlikeComment)| Remove like on a comment. |
|[FGC.KeyValueStoreGetAllKeyValueData](#FGC.KeyValueStoreGetAllKeyValueData)| Get all Key-Value data of the Key Value Store. |
|[FGC.KeyValueStoreGetAllKeys](#FGC.KeyValueStoreGetAllKeys)| Get all Keys of the Key Value Store.  |
|[FGC.KeyValueStoreSetObjectForKey](#FGC.KeyValueStoreSetObjectForKey)| Save data in the Key Value Store. |
|[FGC.KeyValueStoreGetObjectForKey](#FGC.KeyValueStoreGetObjectForKey)| Get data from the Key Value Store. |
|[FGC.KeyValueStoreRemoveObjectForKey](#FGC.KeyValueStoreRemoveObjectForKey)| Remove data from the Key Value Store. |
|[FGC.ShowGUI](#FGC.ShowGUI)| Show the Fresvii GUI. |

-----------------
### <a name ="FGC.SignUp">FGC.SignUp</a>
Creates a user associated with the app. The result is returned by the callback with the arguments of User and Error. The created user ID is encrypted and saved in the local storage.
  
    public static void SignUp(string userName, Action<User, Error> callback) 

#### Parameters
|Name|Type|Description|
|------|------|-----|
|userName|string|Name of the signup user. If there is no user name, set null.|
|description|string|Profile of the signup user. If there is no comment, set null.|
|profileImage|Texture2D|Image of the signup user. If there is no image, set null.|
|callback|Action<User, Error>|Delegate to be called after the signup process|

#### Examples

    {
        ....
        Fresvii.SignUp(”username”, "description",  profileImage,  OnSignUp);   
    }

    void OnSignUp(User user, Error error)
    {
        if (error != null)
        {
            Debug.LogError(error.ToString());
            return;
        }

        Debug.Log(user.name + ", " + user.friend_code + ", " + user.id + ", " + user.created_at + ", " + user.updated_at);        
    }

-----------------
### <a name ="FGC.LogIn">FGC.SignUp</a>
Gets a session token necessary for the user created with SignUp to perform an operation. The acquired access token is retained in the SDK. The result is returned by the callback with the argument of Error. 
  
    public static void LogIn(Action<Error> callback)
    public static void LogIn(int lifeTime, Action<Error> callback)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|userId|Action\<Error\> |Delegate to be called after the signin process|
|userToken|Action\<Error\> |Delegate to be called after the signin process|
|callback|Action\<Error\> |Delegate to be called after the signin process|
|lifeTime|int|Effective time for the access token (in seconds.) If this parameter is not specified, the default value applies.|

#### Example

	{
		.....	

		FGC.LogIn(OnLogIn);
		.....		
	}

    void OnLogIn(Error error)
    {
        if (error != null)
        {
            Debug.LogError(error.ToString());
            return;
        }

        string logMessage = FGC.Instance.Client.AccessToken.Token + ", " +  FGC.Instance.Client.AccessToken.ExpiresAt;
        Debug.Log(logMessage);
    }

-----------------
### <a name ="FGC.LogOut">FGC.LogOut</a>
Lets you log out.

    public static void LogOut()

#### Example

	{
		.....	

		FGC.LogOut();
		.....		
	}

-----------------
### <a name ="FGC.GetSnsAccountList">FGC.GetSnsAccountList</a>
Get the list of SNS authentication information registered for the user. The result is returned by the callback with the arguments of IList of SnsAccount and Error. 
  
     public static void GetSnsAccountList(Action<IList<SnsAccount>, Error> callback)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|callback|Action<IList<FGCSnsAccount>, FGCError> |Delegate to be called after acquiring the SNS authentication information list|
|lifeTime|int|Effective time for the access token (in seconds.) If this parameter is not specified, the default value applies.|

#### Example

    {
        ....
        FGC.GetSnsAccountList(OnGetSnsAccountList);
    }

    void OnGetSnsAccountList(IList<SnsAccount> snsAccountList, Error error)
    {
        if (error != null)
        {
            Debug.LogError(error.ToString());
            return;
        }

        stringlogMessage = "";
        foreach (SnsAccount snsAccount in FGC.Instance.Client.User.SnsAccounts)
            logMessage += snsAccount.Id + ", " + snsAccount.Provider + ", " + snsAccount.Uid + ", " + snsAccount.CreatedAt + ", " + snsAccount.UpdatedAt + "\n";

        Debug.Log(logMessage);
    }

-----------------
### <a name ="FGC.SetSnsAccount">FGC.SetSnsAccount</a>
Save the uie, identifies users in the SNS, acquired through SNS authentication and SNS service name associating with signed in user. The result is returned by the callback with the arguments of SnsAccount and Error. 
  
	public static void SetSnsAccount(string uid, string provider, Action<SnsAccount, Error> callback)
 
#### Parameters
|Name|Type|Description|
|------|------|-----|
|uid|string|ID to identify the user in SNS|
|provider|string|Provider string such as "facebook" or "twitter"|
|accessToken|string|Access token|
|callback|Action<SnsAccount, Error>|Delegate to be called after process|

#### Example

    {
        ....
        FGC.SetSnsAccount("1111", "facebook", "abcdefghijklmn", OnSetSnsAccount);
    }

    void OnSetSnsAccount(SnsAccount snsAccount, Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString();
            Debug.LogError(logMessage);
            return;
        }

        string logMessage = snsAccount.Id + ", " + snsAccount.Provider + ", " + snsAccount.Uid + ", " + snsAccount.CreatedAt + ", " + snsAccount.UpdatedAt;
        Debug.Log(logMessage);
    }

-----------------
### <a name ="FGC.DeleteSnsAccount">FGC.DeleteSnsAccount </a>
Delete the SNS authentication information specified by the id. The result is returned by the callback with the argument of Error. 
  
	public static void DeleteSnsAccount(string id, Action<Error> callback)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|id|string|ID to identify the user in SNS|
|callback|Action\<Error\>|Delegate to be called after process|

#### Example
    {
        ....
        FGC.SetSnsAccount("1111", "facebook", OnSetSnsAccount);
    }

    void OnDeleteSnsAccount(Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString(); ;
            Debug.LogError(logMessage);
            return;
        }

        logMessage = "Delete Success";
        Debug.Log(logMessage);
    }

-----------------
### <a name ="FGC.GetAccount">FGC.GetAccount</a>
Get the signed in users status. The result is returned by the callback with the arguments of User and Error. 
  
    public static void GetAccount(Action<User, Error> callback)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|callback|Action\<Error\>|Delegate to be called after acquisition|

#### Example

    {
        ....
        FGC.GetAccount(OnGetAccount);
    }

    void OnGetAccount(User user, Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString();
            Debug.LogError(logMessage);
            return;
        }

        logMessage = user.Name + ", " + user.FriendCode + ", " + user.Id + ", " + user.CreatedAt + ", " + user.UpdatedAt;
        Debug.Log(logMessage);       
    }

-----------------
### <a name ="FGC.PatchAccount">FGC.PatchAccount</a>
Set up the name and profile image of the signin user. The result is returned by the callback with the arguments of User and Error. 
  
    public static void PatchAccount(string name,　Action<User, Error> callback)
    public static void PatchAccount(Texture2D profileImage,　Action<User, Error> callback)
    public static void PatchAccount(string name,　Texture2D profileImage, Action<User, Error> callback)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|callback|Action\<Error\>|Delegate to be called after setting|

#### Example

    {
        ....
        FGC.PatchAccount("username",　profileImage, OnPatchAccount);
    }

    void OnPatchAccount(User user, Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString();
            Debug.LogError(logMessage);
            return;
        }

        logMessage = user.Name + ", " + user.FriendCode + ", " + user.Id + ", " + user.CreatedAt + ", " + user.UpdatedAt;
        Debug.Log(logMessage);       
    }

-----------------
### <a name ="FGC.GetUser">FGC.GetUser</a>
Get the users status specified by id. The result is returned by the callback with the arguments of User and Error. 
  
    public static void GetUser(string id, Action<User, Error> callback)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|id|string|ID to identify the user in SNS|
|callback|Action\<Error\>|Delegate to be called after acquisition|

#### Example

    {
        ....
        FGC.GetUser(user.id, OnGetUser);
    }

    void OnGetUser(User user, Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString();
            Debug.LogError(logMessage);
            return;
        }

        logMessage = user.Name + ", " + user.FriendCode + ", " + user.Id + ", " + user.CreatedAt + ", " + user.UpdatedAt;
        Debug.Log(logMessage);       
    }


-----------------
### <a name ="FGC.GetUserList">FGC.GetUserList</a>
Get the user list specified by conditions. The result is returned by the callback with the arguments of IList of User and Error. 
  
    public static void GetUserList(string uid, string provider, Action<IList<User>, Error> callback)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|uid|string|ID to identify the user in SNS|
|provider|string|Provider string such as "facebook" or "twitter"|
|callback| Action<IList<User>, Error> |Delegate to be called after process|

#### Example

    {
        ....
        FGC.GetUser(user.id, OnGetUser);
    }

    void OnGetUserList(IList<User> users, Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString();
            Debug.LogError(logMessage);
            return;
        }

        logMessage = "";
        foreach (User user in users)
            logMessage += user.Name + ", " + user.FriendCode + ", " + user.Id + ", " + user.CreatedAt + ", " + user.UpdatedAt + "\n";

        Debug.Log(logMessage);

    }

-----------------
### <a name ="FGC.RegisterRemoteNotification">FGC.RegisterRemoteNotification</a>
Register a notification.
  
    public static void RegisterRemoteNotification(Action<Error> callback)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|callback| Action\<Error\> |Delegate to be called after process|

#### Example

    {
        ....
         FGC.RegisterRemoteNotification(OnRegisterRemoteNotification);
    }

    void OnRegisterRemoteNotification(Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString();
            Debug.LogError(logMessage);
        }
        else
        {
            logMessage = "Success to register notification";
            Debug.Log(logMessage);        
        }
    }

-----------------
### <a name ="FGC.UnregisterRemoteNotification">FGC.UnregisterRemoteNotification</a>
Unregisters a notification.
  
    public static void UnregisterRemoteNotification(Action<Error> callback)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|callback| Action\<Error\> |Delegate to be called after process|

#### Example

    {
        ....
         FGC.UnregisterRemoteNotification(OnRegisterRemoteNotification);
    }

    void OnUnregisterRemoteNotification(Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString();
            Debug.LogError(logMessage);
        }
        else
        {
            logMessage = "Success to unregister notification";
            Debug.Log(logMessage);
        }
    }

-----------------
### <a name ="FGC.GetForumThreads">FGC.GetForumThreads</a>
Get the thread list.
  
	public static void GetForumThreads(Action<IList<Thread>, Error> callback)
	public static void GetForumThreads(uint page, Action<IList<Thread>, Error> callback)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|callback| Action\<IList\<Thread\>, Error\> |Delegate to be called after acquisition|
|page|uint|Page number to be acquired (option.)|

#### Example

    {
        ....
         FGC.GetForumThreads(OnGetForumThreads);
    }

    void OnGetForumThreads(IList<Thread> threads, Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString();
            Debug.LogError(logMessage);
        }

        this.threads = threads;
    }

-----------------
### <a name ="FGC.CreateThread">FGC.CreateThread</a>
Create a new thread.
  
	public static void CreateThread(string text, Action<Thread, Error> callback)
        
#### Parameters
|Name|Type|Description|
|------|------|-----|
|text|string|Comment on the new thread to be created|
|callback| Action\<IList\<Thread\>, Error\> |Delegate to be called after process|

#### Example

    {
        ....
        FGC.CreateThread("thread created " + System.DateTime.Now.ToString(), OnCreateForumThread);
    }

    void OnCreateForumThread(Thread thread, Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString();

            Debug.LogError(logMessage);
        }
    }

-----------------
### <a name ="FGC.DeleteThread">FGC.DeleteThread</a>
Delete a thread. Only the user who created the thread can delete it.
  
	public static void DeleteThread(string id, Action<Error> callback)
        
#### Parameters
|Name|Type|Description|
|------|------|-----|
|callback| Action\<IList\<Thread\>, Error\> |Delegate to be called after process|

#### Example

    {
        ....
        FGC.CreateThread("thread created " + System.DateTime.Now.ToString(), OnCreateForumThread);
    }

    void OnCreateForumThread(Thread thread, Error error)
    {
        if (error != null)
        {
            logMessage = error.ToString();

            Debug.LogError(logMessage);
        }
    }


-----------------
### <a name ="FGC.GetThreadComments">FGC.GetThreadComments</a>
Get the thread comment list.
  
	public static void GetThreadComments(string threadId, Action<IList<Comment>, Error> callback)
        
#### Parameters
|Name|Type|Description|
|------|------|-----|
|threadId|string|ID of the thread whose list is to be acquired|
|callback| Action\<IList\<Comment\>, Error\> |Delegate to be called after acquisition|

#### Example

    {
        ....
        FGC.GetThreadComments(selectedThread.Id, OnGetThreadComments);
    }

    void OnGetThreadComments(IList<Comment> comments, Error error)
    {
        if (error != null)
        {
            logMessage = "Code : " + error.Code + ", Detail : " + error.Detail;
            Debug.LogError(logMessage);
        }

        this.comments = comments;
    }

-----------------
### <a name ="FGC.Subscribe">FGC.Subscribe</a>
Subscribe to a thread.
  
	public static void Subscribe(string threadId, Action<Thread, Error> callback)
        
#### Parameters
|Name|Type|Description|
|------|------|-----|
|threadId|string|ID of the thread to which to subscribe|
|callback| Action\<Thread, Error\> |Delegate to be called after process|

#### Example

    FGC.Subscribe(selectedThread.Id, delegate(Thread _thread, Error _error)
    {
        if (_error != null)
        {
            logMessage = "Subscribe Error\n";
            logMessage += _error.ToString();
            Debug.LogError(logMessage);
        }
        else
        {
            logMessage = "Success subscribe";
        }
    });

-----------------
### <a name ="FGC.Unsubscribe">FGC.Unsubscribe</a>
Unsubscribe from a thread.
  
	public static void Unsubscribe(string threadId, Action<Error> callback)

        
#### Parameters
|Name|Type|Description|
|------|------|-----|
|threadId|string|ID of the thread from which to unsubscribe|
|callback| Action\<Error\> |Delegate to be called after process|

#### Example

	FGC.Unsubscribe(selectedThread.Id, delegate(Error _error)
	{
	    if (_error != null)
	    {
	        logMessage = "Unsubscribe Error\n";
	        logMessage += _error.ToString();
	        Debug.LogError(logMessage);
	    }
	    else
	    {
	        logMessage = "Success unsubscribe";
	    }
	});

-----------------
### <a name ="FGC.AddComment">FGC.AddComment</a>
Add a comment to a thread.
  
	public static void AddComment(string threadId, string text, Action<Comment, Error> callback)        
        
#### Parameters
|Name|Type|Description|
|------|------|-----|
|threadId|string|ID of the thread to which to add a comment|
|text|string|Comment text to be added|
|callback| Action\<Comment, Error\>  |Delegate to be called after process|

#### Example
	
	FGC.AddComment(selectedThread.Id, "Add comment : " + System.DateTime.Now.ToString(), delegate(Comment _comment, Error _error)
	{
	    if (_error != null)
	    {
	        logMessage = "Add comment Error\n";
	        logMessage += logMessage += _error.ToString();
	        Debug.LogError(logMessage);
	    }		    
	});

-----------------
### <a name ="FGC.EditComment">FGC.EditComment</a>
Edit a comment.
  
	public static void EditComment(string commentId, string text, Action<Comment, Error> callback)

        
#### Parameters
|Name|Type|Description|
|------|------|-----|
|commentId|string|ID of the comment to be edited|
|text|string|Comment text to be edited|
|callback| Action\<Comment, Error\>  |Delegate to be called after process|

#### Example
	
	FGC.EditComment(comment.Id, "Edit comment : " + System.DateTime.Now.ToString(), delegate(Comment _comment, Error _error)
        {
            if (_error != null)
            {
                logMessage = "EditComment Error\n";
                logMessage += _error.ToString();
                Debug.LogError(logMessage);
            }
        });

-----------------
### <a name ="FGC.DeleteComment">FGC.DeleteComment</a>
Delete a comment.
  
	public static void DeleteComment(string commentId, Action<Error> callback)

        
#### Parameters
|Name|Type|Description|
|------|------|-----|
|commentId|string|ID of the comment to be deleted|
|callback| Action\<Error\>  |Delegate to be called after process|

#### Example
	
	 FGC.DeleteComment(comment.Id, delegate(Error _error)
        {
            if (_error != null)
            {
                logMessage = "Delete Comment Error\n";
                logMessage += _error.ToString();
                Debug.LogError(logMessage);
            }
        
            FGC.GetThreadComments(selectedThread.Id, OnGetThreadComments);

        });

-----------------
### <a name ="FGC.LikeComment">FGC.LikeComment</a>
Like a comment.
  
	public static void LikeComment(string commentId, Action<Comment, Error> callback)

        
#### Parameters
|Name|Type|Description|
|------|------|-----|
|commentId|string|ID of the comment to be liked|
|callback| Action\<Comment, Error\>  |Delegate to be called after process|

#### Example
	
	{
		....
		FGC.LikeComment(comment.Id, OnLikeComment);
	}
	
	void OnLikeComment(Comment comment, Error error){
			
		if(error != null){
			Debug.LogError(error.ToString());
			return;
		}
		
	}

-----------------
### <a name ="FGC.UnlikeComment">FGC.UnlikeComment</a>
Remove like on a comment.
  
	public static void UnlikeComment(string commentId, Action<Error> callback)

        
#### Parameters
|Name|Type|Description|
|------|------|-----|
|commentId|string|ID of the comment to be unliked|
|callback| Action\<Error\>  |Delegate to be called after process|

#### Example
	
	{
		....
		FGC.UnlikeComment(comment.Id, OnUnlikeComment);
	}
	
	void OnUnlikeComment(Error error){

		if(error != null)
		{
			Debug.LogError(error.ToString());
			return;
		}

	}

-----------------

### <a name ="FGC.ShowGUI">FGC.ShowGUI</a>
Show the GUI, which will be read as a scene.  This method will be called after saving the scene data during the game. GUI shown with a argument is selectable.
  
	 public static void ShowGUI(string returnSceneName)
	 public static void ShowGUI(FresviiGUI.Mode modeFlgs, string returnSceneName)

#### Parameters
|Name|Type|Description|
|------|------|-----|
|modeFlgs|FresviiGUI.Mode|Select from Forum, Leaderboards, MyProfile, and All. More than one mode can be selected.|
|returnSceneName|string|Name of the scene to return when exiting the GUI (pressing the app icon)|

	public enum Mode {Forum = (1 << 0), Leaderboards = (1 << 1), MyProfile = (1 << 2), All = 0xFFFF}; 

#### Example
	
	FGC.ShowGUI("startScene");

	FGC.ShowGUI(FresviiGUI.Mode.Forum | FresviiGUI.Mode.MyProfile, "startScene");

----------

## <a name ="UserClass">User Class</a>

User data class

### Properties
|Type|Name|Description|
|---|---|---|
|string|Name|User name|
|string|FriendCode|Friend code|
|string|Id|User ID|
|string|CreatedAt|Creation date and time|
|string|UpdatedAt|Update date and time|

-----------------

## <a name ="SnsAccount">SnsAccount Class</a>

SNS account class

### Properties
|Type|Name|Description|
|---|---|---|
|string|Id|ID|
|string|Provider|Provider string such as "facebook" or "twitter"|
|string|Uid|User ID|
|string|CreatedAt|Creation date and time|
|string|UpdatedAt|Update date and time|

-----------------

## <a name ="Thread">Thread Class</a>

Thread data class

### Properties
|Type|Name|Description|
|---|---|---|
|string|Id|Thread ID|
|DateTime|CreatedAt|Creation date and time|
|DateTime|UpdateAt|Update date and time|
|uint|CommentCount|Number of comments|
|uint|LikeCount|Number of likes|
|string|UserId|User ID|
|Comment|Comment|
-----------------

## <a name ="Comment">Comment Class</a>

Comment data class

### Properties
|Type|Name|Description|
|---|---|---|
|string|Id|Comment ID|
|DateTime|CreatedAt|Creation date and time|
|DateTime|UpdateAt|Update date and time|
|uint|LikeCount|Number of likes|
|string|ThreadId|Thread ID|
|User|User|User|

--------------------------
### licenses
- [MINIJson](https://gist.github.com/darktable/1411710)  MIT license
- [csharp-sqlite](https://code.google.com/p/csharp-sqlite/) MIT license
- [iTween](http://itween.pixelplacement.com/) iTween is a free, open-source project. As such, it doesn't require any purchase or licensing to be used on commercial projects or otherwise. However, if you use iTween and would like to support the development of the project, please feel free to make a donation.
- [M+ OUTLINE FONTS](http://mplus-fonts.sourceforge.jp/mplus-outline-fonts/) These fonts are free software. 
Unlimited permission is granted to use, copy, and distribute them, with or without modification, either commercially or noncommercially. 
THESE FONTS ARE PROVIDED "AS IS" WITHOUT WARRANTY.