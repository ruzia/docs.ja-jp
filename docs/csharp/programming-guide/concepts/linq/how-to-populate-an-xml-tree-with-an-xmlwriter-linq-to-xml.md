---
title: XmlWriter を使用して XML ツリーを設定する方法 (LINQ to XML) (C#)
description: CreateWriter を使用して XmlWriter を作成し、C# の LINQ to XML で XmlWriter に書き込む方法について説明します。
ms.date: 07/20/2015
ms.assetid: cd5674d1-5c54-4efc-ba68-e23b2875295f
ms.openlocfilehash: 9639c5947583bccf4f8ba427fc8611e181ef1536
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104805"
---
# <a name="how-to-populate-an-xml-tree-with-an-xmlwriter-linq-to-xml-c"></a>XmlWriter を使用して XML ツリーを設定する方法 (LINQ to XML) (C#)
XML ツリーを設定する方法の 1 つは、<xref:System.Xml.Linq.XContainer.CreateWriter%2A> を使用して <xref:System.Xml.XmlWriter> を作成し、この <xref:System.Xml.XmlWriter> に書き込みを行うことです。 XML ツリーには、<xref:System.Xml.XmlWriter> に書き込まれたすべてのノードが挿入されます。  
  
 通常この方法は、[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] と、<xref:System.Xml.XmlWriter> への書き込みを必要とする別のクラス (<xref:System.Xml.Xsl.XslCompiledTransform> など) を併用する場合に使用します。  
  
## <a name="example"></a>例  
 <xref:System.Xml.Linq.XContainer.CreateWriter%2A> は、XSLT 変換を呼び出すときに使用できます。 この例では、XML ツリーを作成し、この XML ツリーから <xref:System.Xml.XmlReader> を作成して、新しいドキュメントを作成します。次に、この新しいドキュメントに書き込むために <xref:System.Xml.XmlWriter> を作成します。 次に、XSLT 変換を呼び出して、<xref:System.Xml.XmlReader> と <xref:System.Xml.XmlWriter> を渡します。 変換が正常に完了すると、新しい XML ツリーに変換結果が挿入されます。  
  
```csharp  
string xslMarkup = @"<?xml version='1.0'?>  
<xsl:stylesheet xmlns:xsl='http://www.w3.org/1999/XSL/Transform' version='1.0'>  
    <xsl:template match='/Parent'>  
        <Root>  
            <C1>  
            <xsl:value-of select='Child1'/>  
            </C1>  
            <C2>  
            <xsl:value-of select='Child2'/>  
            </C2>  
        </Root>  
    </xsl:template>  
</xsl:stylesheet>";  
  
XDocument xmlTree = new XDocument(  
    new XElement("Parent",  
        new XElement("Child1", "Child1 data"),  
        new XElement("Child2", "Child2 data")  
    )  
);  
  
XDocument newTree = new XDocument();  
using (XmlWriter writer = newTree.CreateWriter())  
{  
    // Load the style sheet.  
    XslCompiledTransform xslt = new XslCompiledTransform();  
    xslt.Load(XmlReader.Create(new StringReader(xslMarkup)));  
  
    // Execute the transformation and output the results to a writer.  
    xslt.Transform(xmlTree.CreateReader(), writer);  
}  
  
Console.WriteLine(newTree);  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```xml  
<Root>  
  <C1>Child1 data</C1>  
  <C2>Child2 data</C2>  
</Root>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XContainer.CreateWriter%2A>
- <xref:System.Xml.XmlWriter>
- <xref:System.Xml.Xsl.XslCompiledTransform>
- [XML ツリーの作成 (C#)](./linq-to-xml-overview.md)
