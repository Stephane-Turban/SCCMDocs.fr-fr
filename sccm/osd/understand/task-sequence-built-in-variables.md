---
title: "Variables intégrées de séquence de tâches | Microsoft Docs"
description: "Les variables intégrées de séquence de tâches fournissent des informations sur l’environnement dans lequel la séquence de tâches s’exécute. Elles sont disponibles tout au long de la séquence de tâches."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02bc6bd4-ca53-4e22-8b80-d8ee5fe72567
caps.latest.revision: 15
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c9fb0fa46058c773eec6ac23999357d35d9f970f
ms.openlocfilehash: a75adebfe2bbec8f6fe5206561530a720c0bfbf1


---
# <a name="task-sequence-built-in-variables-in-system-center-configuration-manager"></a>Variables intégrées de séquence de tâches dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Les variables intégrées de séquence de tâches sont fournies par System Center Configuration Manager. Les variables intégrées fournissent des informations sur l'environnement dans lequel la séquence de tâches est exécutée, et leurs valeurs sont disponibles tout au long de la séquence de tâches. En règle générale, les variables intégrées sont initialisées avant que les étapes soient exécutées dans la séquence de tâches. Par exemple, la variable intégrée **_SMSTSLogPath** est une variable d’environnement qui spécifie le chemin que les composants Configuration Manager utilisent pour écrire les fichiers journaux pendant l’exécution de la séquence de tâches ; toutes les étapes de la séquence de tâches peuvent accéder à cette variable d’environnement. Toutefois, certaines variables, telles que &#95;SMSTSCurrentActionName, sont évaluées avant chaque étape. Les valeurs des variables intégrées sont généralement en lecture seule. Les valeurs sont lues uniquement pour les variables intégrées dont le nom commence par un trait de soulignement.  

## <a name="task-sequence-built-in-variable-list"></a>Liste des variables intégrées de la séquence de tâches  
 La liste suivante décrit les variables intégrées qui sont disponibles dans Configuration Manager :  

|Nom de variable intégrée|Description|  
|-----------------------------|-----------------|  
|_OSDDetectedWinDir|À compter de Configuration Manager version 1602, la séquence de tâches analyse les disques durs de l’ordinateur au démarrage de Windows PE pour rechercher une installation antérieure du système d’exploitation. L’emplacement du dossier Windows est stocké dans cette variable. Vous pouvez configurer votre séquence de tâches pour récupérer cette valeur à partir de l’environnement, et l’utiliser pour spécifier le même emplacement du dossier Windows à utiliser pour la nouvelle installation du système d’exploitation.|  
|_OSDDetectedWinDrive|À compter de Configuration Manager version 1602, la séquence de tâches analyse les disques durs de l’ordinateur au démarrage de Windows PE pour rechercher une installation antérieure du système d’exploitation.  L’emplacement d’installation du système d’exploitation sur le disque dur est stocké dans cette variable. Vous pouvez configurer votre séquence de tâches pour récupérer cette valeur à partir de l’environnement, et l’utiliser pour spécifier le même emplacement de disque dur à utiliser pour le nouveau système d’exploitation.|  
|_SMSTSAdvertID|Stocke l'ID unique de déploiement de la séquence de tâches en cours d'exécution. Elle utilise le même format qu’un ID de déploiement de distribution logicielle Configuration Manager. Si la séquence de tâches s'exécute à partir d'un média autonome, cette variable n'est pas définie.<br /><br /> Exemple :<br /><br /> **ABC20001**|  
|_TSAppInstallStatus|la séquence de tâches définit la variable _TSAppInstallStatus avec l'état d'installation de l'application lors de l'étape de séquence de tâches Installer l'application. La séquence de tâches définit la variable sur l'une des valeurs suivantes :<br /><br /> 1.  **Non défini**: valeur définie lorsque l'étape de séquence de tâches Installer l'application n'a pas été exécutée.<br />2.  **Erreur**: valeur définie lorsqu'au moins une application a échoué en raison d'une erreur lors de l'étape de séquence de tâches Installer l'application.<br />3.  **Avertissement**: valeur définie lorsque aucune erreur ne se produit lors de l'étape de séquence de tâches Installer l'application, mais qu'une ou plusieurs applications, ou une dépendance requise, ne se sont pas installées car une spécification n'a pas été satisfaite.<br />4.  **Opération réussie**: valeur définie lorsqu'il n'y a aucune erreur ou aucun avertissement détecté lors de l'étape de séquence de tâches Installer l'application.|  
|_SMSTSBootImageID|Stocke l’ID de package d’images de démarrage Configuration Manager si un package d’images de démarrage est associé à la séquence de tâches en cours d’exécution. La variable ne sera pas définie si aucun package d’images de démarrage Configuration Manager ne lui est associé.<br /><br /> Exemple :<br /><br /> **ABC00001**|  
|_SMSTSBootUEFI|la séquence de tâches définit la variable SMSTSBootUEFI lorsqu'elle détecte un ordinateur en mode UEFI.|  
|_SMSTSClientGUID|Stocke la valeur du GUID du client Configuration Manager. Cette variable n'est pas définie si la séquence de tâches est exécutée à partir d'un média autonome.<br /><br /> Exemple :<br /><br /> **0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c**|  
|_SMSTSCurrentActionName|Spécifie le nom de l'étape de séquence de tâches en cours d'exécution. Cette variable est définie avant que le gestionnaire des séquences de tâches exécute chaque étape individuelle.<br /><br /> Exemple :<br /><br /> **exécuter la ligne de commande**|  
|_SMSTSDownloadOnDemand|Variable définie sur **vrai** si la séquence de tâches en cours est exécutée en mode de téléchargement sur demande, ce qui signifie que le gestionnaire des séquences de tâches télécharge le contenu localement uniquement lorsqu'il doit y accéder.|  
|_SMSTSInWinPE|Cette variable est définie sur **vrai** lorsque l'étape de séquence de tâches en cours est exécutée dans l'environnement Windows PE et elle est définie sur **faux** dans le cas inverse. Vous pouvez tester cette variable de séquence de tâches pour déterminer l'environnement de système d'exploitation actuel.|  
|_SMSTSLastActionRetCode|Stocke le code de retour qui a été renvoyé par la dernière action exécutée. Cette variable peut être utilisée comme une condition pour déterminer si l'étape suivante est exécutée.<br /><br /> Exemple :<br /><br /> **0**|  
|_SMSTSLastActionSucceeded|Cette variable est définie sur **vrai** si la dernière action a réussi et sur **faux** si elle a échoué. Si la dernière action a été ignorée car l'étape était désactivée ou la condition associée était évaluée sur **faux**, cette variable n'est pas réinitialisée, ce qui signifie qu'elle contient toujours la valeur de l'action précédente.|  
|_SMSTSLaunchMode|Spécifie la méthode de lancement de la séquence de tâches. La séquence de tâches peut avoir les valeurs suivantes :<br /><br /> -   **SMS** : spécifie que la séquence de tâches démarre à partir du client Configuration Manager.<br />-   **Disque mémoire flash USB** : spécifie que la séquence de tâches est démarrée à l'aide d'un support USB et que le support USB a été créé sous Windows XP/2003.<br />-   **Disque mémoire flash USB+FORMAT** : spécifie que la séquence de tâches est démarrée à l'aide d'un support USB et que le support USB a été créé sous Windows Vista ou ultérieur.<br />-   **CD** : spécifie que la séquence de tâches est démarrée à l'aide d'un CD.<br />-   **DVD** : spécifie que la séquence de tâches est démarrée à l'aide d'un DVD.<br />-   **PXE** : spécifie que la séquence de tâches est démarrée à partir de PXE.<br />-   **HD** : spécifie que la séquence de tâches a été démarrée à partir d’un disque dur (média préparé uniquement).|  
|_SMSTSLogPath|Stocke le chemin d'accès complet du répertoire des journaux. Cette variable peut servir à déterminer l'emplacement des actions consignées. Cette valeur n'est pas définie si un disque dur n'est pas disponible.|  
|_SMSTSMachineName|Stocke et spécifie le nom de l'ordinateur. Stocke le nom de l'ordinateur que la séquence de tâches utilisera pour consigner tous les messages d'état. Pour modifier le nom d'ordinateur dans le nouveau système d'exploitation, utilisez la variable **OSDComputerName** .<br /><br /> Exemple :<br /><br /> **ABC**|  
|_SMSTSMDataPath|Spécifie le chemin d'accès défini par la variable SMSTSLocalDataDrive. Quand que vous définissez SMSTSLocalDataDrive avant le démarrage de la séquence de tâches, notamment en définissant une variable de regroupement, Configuration Manager définit ensuite la variable _SMSTSMDataPath une fois que la séquence de tâches démarre.|  
|_SMSTSMediaType|Spécifie le type de média qui est utilisé pour démarrer l'installation. Le média de démarrage, le média complet, l'environnement PXE et le média préparé sont des exemples de types de médias.|  
|_SMSTSMP|Stocke le nom ou l’adresse IP d’un point de gestion Configuration Manager.|  
|_SMSTSMPPort|Stocke le numéro de port d’un point de gestion Configuration Manager.<br /><br /> Exemple :<br /><br /> **80**|  
|_SMSTSOrgName|Stocke le nom du titre de la marque qui s'affiche dans la boîte de dialogue de l'interface utilisateur de progression d'une séquence de tâches.<br /><br /> Exemple :<br /><br /> **Organisation XYZ**|  
|_SMSTSOSUpgradeActionReturnCode|Stocke la valeur du code de sortie retourné par le programme d’installation pour indiquer la réussite ou l’échec de l’opération.  Cette variable est définie au cours de l’étape de séquence de tâches Mise à niveau du système d’exploitation des étapes de séquence de tâches. Cela est utile avec l’option de ligne de commande /Compat du programme d’installation de Windows 10.<br /><br /> Exemple :<br /><br /> À l’issue de l’exécution de la commande /Compat, vous pouvez agir dans le cadre d’étapes ultérieures, selon le code de sortie d’échec ou de réussite. En cas de réussite, vous pouvez lancer la mise à niveau. Vous pouvez également définir un indicateur dans l’environnement (par exemple, ajouter un fichier ou définir une clé de Registre), utilisable par la suite pour créer un regroupement d’ordinateurs prêts pour une mise à niveau ou nécessitant une action avant leur mise à niveau.|  
|_SMSTSPackageID|Stocke l'ID de la séquence de tâches en cours d'exécution. Cet ID utilise le même format qu’un ID de package logiciel Configuration Manager.<br /><br /> Exemple :<br /><br /> **HJT00001**|  
|_SMSTSPackageName|Stocke le nom de la séquence de tâches en cours d’exécution spécifié par l’administrateur Configuration Manager au moment où la séquence de tâches est créée.<br /><br /> Exemple :<br /><br /> **Déployer la séquence de tâches de Windows 10**|  
|_SMSTSSetupRollback|Spécifie si le programme d’installation du système d’exploitation a effectué une opération de restauration. Les valeurs des variables peuvent être **true** ou **false**.|  
|_SMSTSRunFromDP|Variable définie sur **vrai** si la séquence de tâches en cours est exécutée en mode exécution à partir du point de distribution, ce qui signifie que le gestionnaire des séquences de tâches obtient des partages de packages requis à partir de points de distribution.|  
|_SMSTSSiteCode|Stocke le code du site Configuration Manager.<br /><br /> Exemple :<br /><br /> **ABC**|  
|_SMSTSType|Spécifie le type de séquence de tâches en cours d'exécution. Il peut afficher les valeurs suivantes :<br /><br /> **1** : indique une séquence de tâches générique.<br /><br /> **2** : indique une séquence de tâches de déploiement du système d'exploitation.|  
|_SMSTSTimezone|La variable _SMSTSTimezone stocke les informations de fuseau horaire au format suivant (sans espaces) :<br /><br /> Biais, StandardBias, DaylightBias, StandardDate.wYear, wMonth, wDayOfWeek, wDay, wHour, wMinute, wSecond, wMilliseconds, DaylightDate.wYear, wMonth, wDayOfWeek, wDay, wHour, wMinute, wSecond, wMilliseconds, StandardName, DaylightName<br /><br /> Exemple :<br /><br /> Pour l'heure de la côte est des États-Unis et du Canada, la valeur serait **300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Heure standard de la côte est, heure d'été de la côte est**|  
|_SMSTSUseCRL|Spécifie si la séquence de tâches utilise la liste de révocation de certificats lors de l'utilisation d'un certificat SSL (Secure Socket Layer) pour communiquer avec le point de gestion.|  
|_SMSTSUserStarted|Spécifie si un utilisateur démarre une séquence de tâches. Cette variable est définie uniquement si la séquence de tâches est démarrée à partir du Centre logiciel. Par exemple, si la variable **_SMSTSLaunchMode** est définie sur **SMS**. La variable peut afficher les valeurs suivantes :<br /><br /> -   **vrai** : spécifie que la séquence de tâches est démarrée manuellement par un utilisateur depuis le Centre logiciel.<br />-   **faux** : spécifie que la séquence de tâches est lancée automatiquement par le planificateur Configuration Manager.|  
|_SMSTSUseSSL|Indique si la séquence de tâches utilise SSL pour communiquer avec le point de gestion Configuration Manager. Si votre site fonctionne en mode natif, la valeur est réglée sur **vrai**.|  
|_SMSTSWTG|spécifie si l'ordinateur s'exécute comme un appareil Windows Go To.|  
|OSDPreserveDriveLetter|À compter de Configuration Manager version 1606, cette variable de séquence de tâches est déconseillée. Pendant le déploiement d’un système d’exploitation, par défaut, le programme d’installation de Windows détermine la meilleure lettre de lecteur à utiliser (généralement, C:). <br /><br />Dans les versions antérieures, la variable OSDPreverveDriveLetter détermine si la séquence de tâches utilise ou non la lettre de lecteur capturée dans le fichier WIM d’image de système d’exploitation au moment où vous appliquez cette image à un ordinateur de destination. Vous pouvez définir la valeur de cette variable sur **False** pour utiliser l’emplacement que vous spécifiez pour le paramètre **Destination** à l’étape de séquence de tâches **Appliquer le système d’exploitation** . Pour plus d'informations, voir [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|OSDSetupAdditionalUpgradeOptions|Depuis Configuration Manager version 1602, vous pouvez utiliser cette variable pour spécifier des options supplémentaires pour la mise à niveau du programme d’installation de Windows.
|SMSTSAssignmentsDownloadInterval|Utilisez cette variable pour spécifier le délai d'attente (exprimé en secondes) entre deux tentatives de téléchargement de la stratégie quand la tentative précédente n'a renvoyé aucune stratégie. Par défaut, le client attend **0** seconde avant une nouvelle tentative.<br /><br /> Cette variable peut être définie à l'aide d'une commande de prédémarrage à partir du média ou de l'environnement PXE.|  
|SMSTSAssignmentsDownloadRetry|Utilisez cette variable pour spécifier le nombre de tentatives de téléchargement de la stratégie par un client quand aucune stratégie n'est trouvée à la première tentative. Par défaut, le client retente **0** fois.<br /><br /> Cette variable peut être définie à l'aide d'une commande de prédémarrage à partir du média ou de l'environnement PXE.|  
|SMSTSAssignUsersMode|Spécifie la façon dont une séquence de tâches associe des utilisateurs à l'ordinateur de destination. Définissez la variable sur l'une des valeurs suivantes.<br /><br /> -   Auto : la séquence de tâches crée une relation entre les utilisateurs spécifiés et l’ordinateur de destination pendant le déploiement du système d’exploitation sur l’ordinateur de destination.<br />-   En attente : la séquence de tâches crée une relation entre les utilisateurs spécifiés et l’ordinateur de destination, mais attend l’approbation de l’utilisateur administratif avant de définir la relation.<br />-   Désactivé : la séquence de tâches n’associe pas d’utilisateurs à l’ordinateur de destination pendant le déploiement du système d’exploitation.|  
|SMSTSDownloadAbortCode|Cette variable contient la valeur du code d’abandon pour le téléchargeur du programme externe (spécifié dans la variable SMSTSDownloadProgram). Si le programme retourne un code d’erreur égal à la valeur de la variable SMSTSDownloadAbortCode, le téléchargement du contenu échoue et aucune autre méthode de téléchargement n’est tentée.
|SMSTSDownloadProgram|Cette variable permet de spécifier un Autre fournisseur de contenu, un téléchargeur utilisé pour télécharger du contenu à la place du programme de téléchargement Configuration Manager par défaut, pour la séquence tâches. Dans le cadre du processus de téléchargement de contenu, la séquence de tâches examine si la variable indique un programme de téléchargement spécifique. Si c'est le cas, la séquence de tâches l'exécute pour procéder au téléchargement.|  
|SMSTSDownloadRetryCount|Cette variable permet de spécifier le nombre de fois que Configuration Manager tente de télécharger du contenu à partir d’un point de distribution. Par défaut, le client effectue **2** nouvelles tentatives.|  
|SMSTSDownloadRetryDelay|Cette variable permet de spécifier le délai d’attente de Configuration Manager (en secondes) avant qu’il tente à nouveau de télécharger du contenu à partir d’un point de distribution. Par défaut, le client attend **15** secondes avant une nouvelle tentative.|  
|SMSTSErrorDialogTimeout|Lorsqu'une erreur se produit dans une séquence de tâches, une boîte de dialogue s'affiche et est fermée automatiquement après un nombre de secondes spécifié par cette variable. Par défaut, la boîte de dialogue disparaît automatiquement après **900** secondes (15 minutes).|  
|TSErrorOnWarning|Utilisez cette variable pour spécifier si le moteur de séquence de tâches considère qu'un avertissement détecté constitue une erreur durant l'étape de séquence de tâches Installation de l'application. La séquence de tâches affecte la valeur **Warning** à la variable _TSAppInstallStatus quand une ou plusieurs applications, ou une dépendance nécessaire, n'ont pas été installées car une exigence n'a pas été remplie. Lorsque vous affectez la valeur **True** à la variable TSErrorOnWarning et que la variable _TSAppInstallStatus a la valeur Warning, elle est traitée comme une erreur. La valeur **False** est le comportement par défaut.|  
|SMSTSLanguageFolder|utilisez cette variable pour modifier la langue d'affichage d'une image de démarrage indépendante de la langue.|  
|SMSTSLocalDataDrive|Spécifie l'emplacement de stockage des fichiers temporaires sur l'ordinateur de destination lors de l'exécution de la séquence de tâches.<br /><br /> Cette variable doit être définie avant le démarrage de la séquence de tâches, notamment en définissant une variable de regroupement. Une fois que la séquence de tâches démarre, Configuration Manager définit la variable _SMSTSMDataPath.|  
|SMSTSMPListRequestTimeout|Cette variable permet de spécifier le délai d’attente (en millisecondes) d’une séquence de tâches avant qu’elle tente à nouveau d’installer une application ou une mise à jour logicielle après l’échec de la récupération de la liste de points de gestion auprès des services de localisation. Par défaut, la séquence de tâches attend 60 000 millisecondes (60 secondes) avant de retenter d'exécuter l'étape et elle effectue jusqu'à trois nouvelles tentatives. Cette variable s’applique uniquement aux étapes de la séquence de tâches d’installation d’application et de mises à jour logicielles.|  
|SMSTSMPListRequestTimeoutEnabled|Cette variable permet d’activer les demandes MPList répétées pour actualiser le client s’il ne se trouve pas sur l’intranet. <br />Par défaut, cette valeur est définie sur True. Si des clients se trouvent sur Internet, vous pouvez définir cette variable sur False pour éviter des retards inutiles. Cette variable s’applique uniquement aux étapes de la séquence de tâches relatives à l’installation de l’application et à l’installation des mises à jour logicielles.|  
|SMSTSPeerDownload|Utilisez cette variable pour permettre au client d’utiliser la mise en cache d’homologue Windows PE.<br /><br /> Exemple :<br /><br /> SMSTSPeerDownload = **TRUE** active cette fonctionnalité.|  
|SMSTSPeerRequestPort|Utilisez cette variable pour le cache d’homologue Windows PE afin de spécifier un port réseau personnalisé à utiliser pour la diffusion initiale quand vous n’utilisez pas les ports par défaut configurés dans les paramètres du client (8004).|  
|SMSTSPersistContent|utilisez cette variable pour conserver temporairement le contenu du cache de la séquence de tâches.|  
|SMSTSPostAction|Spécifie une commande exécutée une fois la séquence de tâches terminée. Par exemple, vous pouvez utiliser cette variable pour spécifier un script qui active des filtres d'écriture sur les appareils intégrés après que la séquence de tâches a déployé un système d'exploitation sur l'appareil.|  
|SMSTSPreferredAdvertID|Force l'exécution d'un déploiement ciblé spécifique sur l'ordinateur de destination. Cela peut être défini à l'aide d'une commande de prédémarrage à partir de média ou PXE. Si cette variable est définie, la séquence de tâches se substitue à tous les déploiements requis.|  
|SMSTSPreserveContent|Cette variable marque le contenu dans la séquence de tâches pour qu’il soit conservé dans le cache du client Configuration Manager après le déploiement. Elle se distingue de SMSTSPersisContent, qui conserve uniquement le contenu pendant la durée de la séquence de tâches et utilise le cache de la séquence de tâches, et non le cache du client Configuration Manager.<br /><br /> Exemple :<br /><br /> SMSTSPreserveContent = **TRUE** active cette fonctionnalité.|  
|SMSTSRebootDelay|Spécifie le nombre de secondes à attendre avant que l'ordinateur redémarre. Le gestionnaire des séquences de tâches affiche une boîte de dialogue de notification avant le redémarrage si cette variable n'est pas définie sur 0.<br /><br /> Exemples :<br /><br /> **0**<br /><br /> **30**|  
|SMSTSRebootMessage|Spécifie le message à afficher dans la boîte de dialogue de fermeture lorsqu'un redémarrage est demandé. Si vous ne définissez pas cette variable, un message par défaut apparaît.<br /><br /> Exemple :<br /><br /> **Cet ordinateur est en cours de redémarrage par le gestionnaire des séquences de tâches**.|  
|SMSTSRebootRequested|Indique qu'un redémarrage est demandé après que l'étape de séquence de tâches en cours est terminée. Si un redémarrage est nécessaire, définissez simplement cette variable sur **vrai**et le gestionnaire des séquences de tâches redémarrera l'ordinateur après cette étape de la séquence de tâches. L'étape de séquence de tâches doit définir cette variable de séquence de tâches si elle exige un redémarrage pour finaliser l'étape de la séquence de tâches. Après le redémarrage de l'ordinateur, la séquence de tâches continue d'être exécutée à partir de l'étape de séquence de tâches suivante.|  
|SMSTSRetryRequested|Demande une nouvelle tentative après la fin de l'étape de séquence de tâches en cours. Si cette variable de séquence de tâches est définie, la variable **SMSTSRebootRequested** doit également être définie sur **vrai**. Après le redémarrage de l'ordinateur, le gestionnaire des séquences de tâches exécute à nouveau la même étape de la séquence de tâches.|  
|SMSTSSoftwareUpdateScanTimeout| Permet de contrôler le délai d’attente pendant la recherche de mises à jour logicielles à l’étape de la séquence de tâches [Installer les mises à jour logicielles](task-sequence-steps.md#BKMK_InstallSoftwareUpdates). Par exemple, vous pouvez accroître la valeur par défaut si vous avez un grand nombre de mises à jour à installer. La valeur par défaut est de 30 minutes. |
|SMSTSUDAUsers|Spécifie l'utilisateur principal de l'ordinateur de destination. Spécifiez les utilisateurs en utilisant le format suivant. Séparez plusieurs utilisateurs à l'aide d'une virgule (,).<br /><br /> Exemple :<br /><br /> **domaine\utilisateur1, domaine\utilisateur2, domaine\utilisateur3**<br /><br /> Pour plus d’informations sur l’association d’utilisateurs à l’ordinateur de destination, consultez [Associer des utilisateurs à un ordinateur de destination](../get-started/associate-users-with-a-destination-computer.md).|  
|SMSTSWaitForSecondReboot|À compter de Configuration Manager version 1602, cette variable de séquence de tâches facultative est disponible pour vous aider à contrôler le comportement du client quand l’installation d’une mise à jour logicielle nécessite deux redémarrages. Cette variable doit être définie avant l’étape [Installer les mises à jour logicielles](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) pour empêcher qu’une séquence de tâches échoue en raison d’un second redémarrage lié à l’installation d’une mise à jour logicielle.<br /><br /> Définissez la valeur de SMSTSWaitForSecondReboot en secondes pour spécifier la durée pendant laquelle la séquence de tâches s’interrompt pendant l’étape d’installation de mises à jour logicielles lors du redémarrage de l’ordinateur afin de prévoir un temps suffisant en cas de deuxième redémarrage. <br />Par exemple, si vous définissez SMSTSWaitForSecondReboot sur 600, la séquence de tâches est suspendue pendant 10 minutes après un redémarrage, avant l’exécution d’étapes supplémentaires de la séquence de tâches. Cela est utile quand des centaines de mises à jour logicielles sont installées en une seule étape de séquence de tâches d’installation de mises à jour logicielles.|  



<!--HONumber=Dec16_HO3-->

