---
title: 遅延実行の例 (C#)
description: 遅延実行とレイジー評価が C# での LINQ to XML クエリの実行にどのように影響するかについて確認します。
ms.date: 07/20/2015
ms.assetid: 50f4fbac-81fe-4f26-aedf-506e21419b19
ms.openlocfilehash: 65ba4cc150f2fc9d8f44aee352987ea0eeaab0a5
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103955"
---
# <a name="deferred-execution-example-c"></a>遅延実行の例 (C#)
このトピックでは、遅延実行とレイジー評価が LINQ to XML クエリの実行にどのように影響するかについて説明します。  
  
## <a name="example"></a>例  
 遅延実行を利用する拡張メソッドの使用時における実行順序の例を次に示します。 この例では、3 つの文字列の配列を宣言します。 次に、`ConvertCollectionToUpperCase` によって返されるコレクションを反復処理します。  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source {0}", str);  
            yield return str.ToUpper();  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        var q = from str in stringArray.ConvertCollectionToUpperCase()  
                select str;  
  
        foreach (string str in q)  
            Console.WriteLine("Main: str {0}", str);  
    }  
}  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```output  
ToUpper: source abc  
Main: str ABC  
ToUpper: source def  
Main: str DEF  
ToUpper: source ghi  
Main: str GHI  
```  
  
 `ConvertCollectionToUpperCase` によって返されるコレクションの反復処理時、各アイテムはソース文字列の配列から取得され、次のアイテムがソース文字列の配列から取得される前に大文字に変換されることに注意してください。  
  
 返されるコレクションの各アイテムが `foreach` の `Main` ループで処理されるまで、文字列の配列全体は大文字に変換されないことを確認できます。  
  
 このチュートリアルの次のトピックでは、クエリの連結について説明します。  
  
- [クエリの連結の例 (C#)](./chaining-queries-example.md)  
  
## <a name="see-also"></a>関連項目

- [チュートリアル: クエリの連結 (C#)](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)
