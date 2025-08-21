### デバイスを迅速にハイブリッド Azure AD に参加させる 

### 手順1：まず Azure AD の状態を確認する 

コマンド プロンプトで次のコマンドを入力します：
dsregcmd /status

以下の図は、ハイブリッド Azure AD に参加していない状態を示しています。
```
+----------------------------------------------------------------------+
| Device State                                                         |
+----------------------------------------------------------------------+
             AzureAdJoined : NO <-
          EnterpriseJoined : NO
              DomainJoined : YES
                DomainName : HYBRIDADFS
+----------------------------------------------------------------------+
```

### デバイスの状態

AzureAdJoined | EnterpriseJoined | DomainJoined | Device Status
-- | -- | -- | --
yes | No | No | Microsoft Entra connection established
No | No | yes | Domain joined
yes | No | yes | Microsoft Entra hybrid join completed
No | yes | yes | A local DRS connection has been established

AzureAdJoined ：デバイスが Microsoft Entra ID に参加している場合、状態は「Yes」に設定します。それ以外の場合は「No」とします。

EnterpriseJoined ：デバイスがオンプレミスの Active Directory (AD) に参加している場合、状態は「Yes」に設定します。デバイスは同時に EnterpriseJoined と AzureAdJoined になることはできません。

DomainJoined ：デバイスがドメイン (Active Directory) に参加している場合、状態は「Yes」に設定します。

DomainName ：デバイスがドメインに参加している場合、状態はドメイン名を設定します。


### 手順2：タスクスケジューラを使用して、デバイスをハイブリッド Azure AD に再登録します。

以下の手順に従ってください:

 

- タスクスケジューラを管理者として実行します。


<img width="164" alt="task-scheduler" src="https://github.com/user-attachments/assets/91b7740e-2d2d-4a0e-bbdd-c0422617fa41" />

-  Task Scheduler Library > Microsoft > Windows > Workplace Join and manually start the task “Automatic-Device-Join“.

<img width="432" alt="rejoin" src="https://github.com/user-attachments/assets/648b2179-c76c-4ab1-a2ad-675946d85ed0" />

- Type the command **dsregcmd /leave**  and **dsregcmd /join**  the device will rejoin again. 

 ### 手順3：しばらく待ってから dsregcmd /status を入力します。実行すると、状態が 「Joined」 と表示されます。

```
+----------------------------------------------------------------------+
| Device State                                                         |
+----------------------------------------------------------------------+
             AzureAdJoined : YES  <-
          EnterpriseJoined : NO
              DomainJoined : YES  
                DomainName : HYBRIDADFS
+----------------------------------------------------------------------+
```


**これは、デバイスを迅速にハイブリッド Azure AD に参加させる方法です！**
