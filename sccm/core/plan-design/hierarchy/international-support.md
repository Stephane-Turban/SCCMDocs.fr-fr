---
title: Prise en charge internationale | Microsoft Docs
description: "Configurez System Center Configuration Manager pour respecter des exigences internationales spécifiques."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 37e45e604e89d3ce280bb2bff47d4a55b6cdfaf8


---
# <a name="international-support-in-system-center-configuration-manager"></a>Prise en charge internationale dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les sections suivantes fournissent des détails techniques pour vous aider à configurer System Center Configuration Manager pour en assurer la conformité à des exigences internationales spécifiques.  

## <a name="gb18030-requirements"></a>Normes GB18030  
 Configuration Manager respecte les normes GB18030 pour permettre son utilisation en Chine. Un déploiement de Configuration Manager doit disposer des configurations suivantes pour respecter les exigences des normes GB18030 :  

-   Chaque ordinateur serveur de site et chaque ordinateur SQL Server utilisés avec Configuration Manager doivent utiliser un système d’exploitation chinois.  

-   Chaque base de données de site et chaque instance de SQL Server dans la hiérarchie doit utiliser le même classement et doit correspondre à l'un des éléments suivants :  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Ces classements de base de données constituent une exception à la configuration requise décrite dans [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Vous devez placer un fichier portant le nom **GB18030.SMS** dans le dossier racine du volume du système de chaque ordinateur du serveur de site dans la hiérarchie. Ce fichier ne contient pas de données et peut être un fichier texte vide, nommé pour répondre à cette exigence.  



<!--HONumber=Dec16_HO3-->

