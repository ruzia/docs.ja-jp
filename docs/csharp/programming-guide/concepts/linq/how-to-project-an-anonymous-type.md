---
title: 匿名型を射影する方法 (C#)
description: C# の匿名型にクエリを射影する方法について説明します。 少し使用するだけのために新しい型を作成するより、匿名型を使用する方が簡単です。
ms.date: 07/20/2015
ms.assetid: 5cb9be13-5ac4-4373-a034-b3520a5b2dec
ms.openlocfilehash: 6598796a4ba95362340f2551b1da6ac6d857eaae
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104630"
---
# <a name="how-to-project-an-anonymous-type-c"></a>匿名型を射影する方法 (C#)
短期間しか使用しないことがわかっている新しい型にクエリを射影することが必要になる場合があります。 単に射影で使用するために新しい型を作成するのは大きな負担です。 この場合は、匿名型に射影する方法が効率的です。 匿名型を使用すると、クラス名を指定することなくクラスを定義し、そのクラスのオブジェクトを宣言して初期化できます。  
  
 匿名型とは、*タプル*の数学的概念を C# で実装したものです。 タプルという数学用語は、1 タプル、2 タプル、3 タプル、4 タプル、5 タプル、n タプルという数列に基づいています。 組とは、それぞれが特定の型を持つオブジェクトの有限のシーケンスを意味します。 名前と値のペアの一覧と呼ばれることもあります。 たとえば、[サンプル XML ファイル: 一般的な購買発注書 (LINQ to XML)](./sample-xml-file-typical-purchase-order-linq-to-xml-1.md) の XML ドキュメントのアドレス コンテンツは次のように表されます。  
  
```text  
Name: Ellen Adams  
Street: 123 Maple Street  
City: Mill Valley  
State: CA  
Zip: 90952  
Country: USA  
```  
  
 匿名型のインスタンスを作成するときは、注文 n のタプルを作成すると考えると簡単です。 `select` 句でタプルを作成するクエリを記述すると、そのクエリからタプルの `IEnumerable` が返されます。  
  
## <a name="example"></a>例  
 この例では、`select` 句で匿名型を射影しています。 さらに、`var` を使用して `IEnumerable` オブジェクトを作成しています。 `foreach` ループ内では、繰り返し変数が、クエリ式で作成された匿名型のインスタンスになります。  
  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル:顧客と注文 (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md)」。  
  
```csharp  
XElement custOrd = XElement.Load("CustomersOrders.xml");  
var custList =  
    from el in custOrd.Element("Customers").Elements("Customer")  
    select new {  
        CustomerID = (string)el.Attribute("CustomerID"),  
        CompanyName = (string)el.Element("CompanyName"),  
        ContactName = (string)el.Element("ContactName")  
    };  
foreach (var cust in custList)  
    Console.WriteLine("{0}:{1}:{2}", cust.CustomerID, cust.CompanyName, cust.ContactName);  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```output  
GREAL:Great Lakes Food Market:Howard Snyder  
HUNGC:Hungry Coyote Import Store:Yoshi Latimer  
LAZYK:Lazy K Kountry Store:John Steel  
LETSS:Let's Stop N Shop:Jaime Yorres  
```  
  