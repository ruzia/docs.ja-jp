---
ms.openlocfilehash: 32c7f4e9e4736145f9275b74f34c04404e7c770a
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394114"
---
### <a name="caching-microsoftextensionscachingsqlserver-uses-new-sqlclient-package"></a><span data-ttu-id="39555-101">キャッシュ:Microsoft.Extensions.Caching.SqlServer で新しい SqlClient パッケージを使用</span><span class="sxs-lookup"><span data-stu-id="39555-101">Caching: Microsoft.Extensions.Caching.SqlServer uses new SqlClient package</span></span>

<span data-ttu-id="39555-102">`Microsoft.Extensions.Caching.SqlServer` パッケージでは、`System.Data.SqlClient` パッケージの代わりに、新しい `Microsoft.Data.SqlClient` パッケージが使用されます。</span><span class="sxs-lookup"><span data-stu-id="39555-102">The `Microsoft.Extensions.Caching.SqlServer` package will use the new `Microsoft.Data.SqlClient` package instead of `System.Data.SqlClient` package.</span></span> <span data-ttu-id="39555-103">この変更により、動作のわずかな破壊的変更が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="39555-103">This change could cause slight behavioral breaking changes.</span></span> <span data-ttu-id="39555-104">詳細については、「[Introducing the new Microsoft.Data.SqlClient (新しい Microsoft.Data.SqlClient の導入)](https://devblogs.microsoft.com/dotnet/introducing-the-new-microsoftdatasqlclient/)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="39555-104">For more information, see [Introducing the new Microsoft.Data.SqlClient](https://devblogs.microsoft.com/dotnet/introducing-the-new-microsoftdatasqlclient/).</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="39555-105">導入されたバージョン</span><span class="sxs-lookup"><span data-stu-id="39555-105">Version introduced</span></span>

<span data-ttu-id="39555-106">3.0</span><span class="sxs-lookup"><span data-stu-id="39555-106">3.0</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="39555-107">以前の動作</span><span class="sxs-lookup"><span data-stu-id="39555-107">Old behavior</span></span>

<span data-ttu-id="39555-108">`Microsoft.Extensions.Caching.SqlServer` パッケージで、`System.Data.SqlClient` パッケージが使用されていました。</span><span class="sxs-lookup"><span data-stu-id="39555-108">The `Microsoft.Extensions.Caching.SqlServer` package used the `System.Data.SqlClient` package.</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="39555-109">新しい動作</span><span class="sxs-lookup"><span data-stu-id="39555-109">New behavior</span></span>

<span data-ttu-id="39555-110">`Microsoft.Extensions.Caching.SqlServer` で、`Microsoft.Data.SqlClient` パッケージが使用されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="39555-110">`Microsoft.Extensions.Caching.SqlServer` is now using the `Microsoft.Data.SqlClient` package.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="39555-111">変更理由</span><span class="sxs-lookup"><span data-stu-id="39555-111">Reason for change</span></span>

<span data-ttu-id="39555-112">`Microsoft.Data.SqlClient` は、`System.Data.SqlClient` から構築された新しいパッケージです。</span><span class="sxs-lookup"><span data-stu-id="39555-112">`Microsoft.Data.SqlClient` is a new package that is built off of `System.Data.SqlClient`.</span></span> <span data-ttu-id="39555-113">今後、機能の新しい動作はすべてこのパッケージで実行されます。</span><span class="sxs-lookup"><span data-stu-id="39555-113">It's where all new feature work will be done from now on.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="39555-114">推奨される操作</span><span class="sxs-lookup"><span data-stu-id="39555-114">Recommended action</span></span>

<span data-ttu-id="39555-115">`Microsoft.Extensions.Caching.SqlServer` パッケージによって返される型を使用し、それらを `System.Data.SqlClient` の型にキャストしている場合を除き、この破壊的変更について気にする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="39555-115">Customers shouldn't need to worry about this breaking change unless they were using types returned by the `Microsoft.Extensions.Caching.SqlServer` package and casting them to `System.Data.SqlClient` types.</span></span> <span data-ttu-id="39555-116">たとえば、`DbConnection` を[以前の SqlConnection 型](xref:System.Data.SqlClient.SqlConnection)にキャストしている場合は、キャストを新しい `Microsoft.Data.SqlClient.SqlConnection` 型に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="39555-116">For example, if someone was casting a `DbConnection` to the [old SqlConnection type](xref:System.Data.SqlClient.SqlConnection), they would need to change the cast to the new `Microsoft.Data.SqlClient.SqlConnection` type.</span></span> 

#### <a name="category"></a><span data-ttu-id="39555-117">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="39555-117">Category</span></span>

<span data-ttu-id="39555-118">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="39555-118">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="39555-119">影響を受ける API</span><span class="sxs-lookup"><span data-stu-id="39555-119">Affected APIs</span></span>

<span data-ttu-id="39555-120">なし</span><span class="sxs-lookup"><span data-stu-id="39555-120">None</span></span>

<!-- 

#### Affected APIs

Not detectable via API analysis

-->