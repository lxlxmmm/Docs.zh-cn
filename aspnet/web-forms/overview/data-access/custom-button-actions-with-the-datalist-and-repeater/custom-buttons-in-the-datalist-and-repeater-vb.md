---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
title: "DataList 和转发器 (VB) 中的自定义按钮 |Microsoft 文档"
author: rick-anderson
description: "在本教程中，我们将生成一个接口，使用中继器要列出各个类别在系统中，每个类别都提供一个按钮以显示其 associ..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/13/2006
ms.topic: article
ms.assetid: 1afdb14d-6e49-4e1f-aead-2934730d472e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 14e245f5fd25079b4ee1dee566ca451f955a8b25
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="custom-buttons-in-the-datalist-and-repeater-vb"></a><span data-ttu-id="fe504-103">DataList 和转发器 (VB) 中的自定义按钮</span><span class="sxs-lookup"><span data-stu-id="fe504-103">Custom Buttons in the DataList and Repeater (VB)</span></span>
====================
<span data-ttu-id="fe504-104">通过[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="fe504-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="fe504-105">[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_VB.exe)或[下载 PDF](custom-buttons-in-the-datalist-and-repeater-vb/_static/datatutorial46vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="fe504-105">[Download Sample App](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_VB.exe) or [Download PDF](custom-buttons-in-the-datalist-and-repeater-vb/_static/datatutorial46vb1.pdf)</span></span>

> <span data-ttu-id="fe504-106">在本教程中我们将生成一个接口，使用中继器要列出各个类别在系统中，每个类别都提供一个按钮以显示如何使用其相关的产品。</span><span class="sxs-lookup"><span data-stu-id="fe504-106">In this tutorial we'll build an interface that uses a Repeater to list the categories in the system, with each category providing a button to show its associated products using a BulletedList control.</span></span>


## <a name="introduction"></a><span data-ttu-id="fe504-107">介绍</span><span class="sxs-lookup"><span data-stu-id="fe504-107">Introduction</span></span>

<span data-ttu-id="fe504-108">在过去的十七 DataList 和转发器教程，我们制作了只读示例和编辑和删除示例。</span><span class="sxs-lookup"><span data-stu-id="fe504-108">Throughout the past seventeen DataList and Repeater tutorials, we ve created both read-only examples and editing and deleting examples.</span></span> <span data-ttu-id="fe504-109">为了便于编辑和删除于 DataList 中的功能，我们将按钮添加到 DataList s `ItemTemplate` ，单击时，导致回发，并引发与按钮 s 对应 DataList 事件`CommandName`属性。</span><span class="sxs-lookup"><span data-stu-id="fe504-109">To facilitate editing and deleting capabilities within a DataList, we added buttons to the DataList s `ItemTemplate` that, when clicked, caused a postback and raised a DataList event corresponding to the button s `CommandName` property.</span></span> <span data-ttu-id="fe504-110">例如，添加到按钮`ItemTemplate`与`CommandName`编辑属性值将使 DataList s`EditCommand`为回发，则对触发另一个使用`CommandName`删除引发`DeleteCommand`。</span><span class="sxs-lookup"><span data-stu-id="fe504-110">For example, adding a button to the `ItemTemplate` with a `CommandName` property value of Edit causes the DataList s `EditCommand` to fire on postback; one with the `CommandName` Delete raises the `DeleteCommand`.</span></span>

<span data-ttu-id="fe504-111">除了要编辑和删除按钮，DataList 和转发器控件可以还包括按钮、 LinkButtons 或 ImageButtons，单击时，执行某些自定义服务器端逻辑。</span><span class="sxs-lookup"><span data-stu-id="fe504-111">In addition to Edit and Delete buttons, the DataList and Repeater controls can also include Buttons, LinkButtons, or ImageButtons that, when clicked, perform some custom server-side logic.</span></span> <span data-ttu-id="fe504-112">在本教程中我们将生成一个接口，使用中继器列出系统中的类别。</span><span class="sxs-lookup"><span data-stu-id="fe504-112">In this tutorial we'll build an interface that uses a Repeater to list the categories in the system.</span></span> <span data-ttu-id="fe504-113">转发器将针对每个类别，包括一个按钮以显示使用如何的产品的类别 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="fe504-113">For each category, the Repeater will include a button to show the category s associated products using a BulletedList control (see Figure 1).</span></span>


<span data-ttu-id="fe504-114">[![单击显示产品链接显示项目符号列表中的类别 s 产品](custom-buttons-in-the-datalist-and-repeater-vb/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fe504-114">[![Clicking the Show Products Link Displays the Category s Products in a Bulleted List](custom-buttons-in-the-datalist-and-repeater-vb/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image1.png)</span></span>

<span data-ttu-id="fe504-115">**图 1**： 单击显示的产品链接显示项目符号列表中的 s 产品类别 ([单击以查看实际尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fe504-115">**Figure 1**: Clicking the Show Products Link Displays the Category s Products in a Bulleted List ([Click to view full-size image](custom-buttons-in-the-datalist-and-repeater-vb/_static/image3.png))</span></span>


## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a><span data-ttu-id="fe504-116">步骤 1： 添加自定义按钮教程 Web 页</span><span class="sxs-lookup"><span data-stu-id="fe504-116">Step 1: Adding the Custom Button Tutorial Web Pages</span></span>

<span data-ttu-id="fe504-117">我们探讨如何添加自定义按钮之前，让 s 先花点时间在本教程中我们将需要我们网站项目中创建 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="fe504-117">Before we look at how to add a custom button, let s first take a moment to create the ASP.NET pages in our website project that we'll need for this tutorial.</span></span> <span data-ttu-id="fe504-118">首先，通过添加一个名为的新文件夹`CustomButtonsDataListRepeater`。</span><span class="sxs-lookup"><span data-stu-id="fe504-118">Start by adding a new folder named `CustomButtonsDataListRepeater`.</span></span> <span data-ttu-id="fe504-119">接下来，将以下两个 ASP.NET 页添加到该文件夹，并确保将每个包含网页相关联`Site.master`母版页：</span><span class="sxs-lookup"><span data-stu-id="fe504-119">Next, add the following two ASP.NET pages to that folder, making sure to associate each page with the `Site.master` master page:</span></span>

- `Default.aspx`
- `CustomButtons.aspx`


![有关自定义的按钮相关教程添加的 ASP.NET 页面](custom-buttons-in-the-datalist-and-repeater-vb/_static/image4.png)

<span data-ttu-id="fe504-121">**图 2**： 添加 ASP.NET 页的自定义按钮相关教程</span><span class="sxs-lookup"><span data-stu-id="fe504-121">**Figure 2**: Add the ASP.NET Pages for the Custom Buttons-Related Tutorials</span></span>


<span data-ttu-id="fe504-122">在其他文件夹中，如`Default.aspx`中`CustomButtonsDataListRepeater`文件夹将在其部分中列出这些教程。</span><span class="sxs-lookup"><span data-stu-id="fe504-122">Like in the other folders, `Default.aspx` in the `CustomButtonsDataListRepeater` folder will list the tutorials in its section.</span></span> <span data-ttu-id="fe504-123">回想一下，`SectionLevelTutorialListing.ascx`用户控件提供此功能。</span><span class="sxs-lookup"><span data-stu-id="fe504-123">Recall that the `SectionLevelTutorialListing.ascx` User Control provides this functionality.</span></span> <span data-ttu-id="fe504-124">此用户将控件添加到`Default.aspx`通过从解决方案资源管理器拖到页面上的设计视图拖动。</span><span class="sxs-lookup"><span data-stu-id="fe504-124">Add this User Control to `Default.aspx` by dragging it from the Solution Explorer onto the page s Design view.</span></span>


<span data-ttu-id="fe504-125">[![SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](custom-buttons-in-the-datalist-and-repeater-vb/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="fe504-125">[![Add the SectionLevelTutorialListing.ascx User Control to Default.aspx](custom-buttons-in-the-datalist-and-repeater-vb/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image5.png)</span></span>

<span data-ttu-id="fe504-126">**图 3**： 添加`SectionLevelTutorialListing.ascx`用户控件`Default.aspx`([单击以查看实际尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image7.png))</span><span class="sxs-lookup"><span data-stu-id="fe504-126">**Figure 3**: Add the `SectionLevelTutorialListing.ascx` User Control to `Default.aspx` ([Click to view full-size image](custom-buttons-in-the-datalist-and-repeater-vb/_static/image7.png))</span></span>


<span data-ttu-id="fe504-127">最后，将页添加到的条目为`Web.sitemap`文件。</span><span class="sxs-lookup"><span data-stu-id="fe504-127">Lastly, add the pages as entries to the `Web.sitemap` file.</span></span> <span data-ttu-id="fe504-128">具体而言，分页和排序后添加以下标记，使用 DataList 和转发器`<siteMapNode>`:</span><span class="sxs-lookup"><span data-stu-id="fe504-128">Specifically, add the following markup after the Paging and Sorting with the DataList and Repeater `<siteMapNode>`:</span></span>


[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample1.xml)]

<span data-ttu-id="fe504-129">在更新后`Web.sitemap`，花些时间查看通过浏览器网站的教程。</span><span class="sxs-lookup"><span data-stu-id="fe504-129">After updating `Web.sitemap`, take a moment to view the tutorials website through a browser.</span></span> <span data-ttu-id="fe504-130">在左侧菜单现在包括用于编辑、 插入和删除教程的项。</span><span class="sxs-lookup"><span data-stu-id="fe504-130">The menu on the left now includes items for the editing, inserting, and deleting tutorials.</span></span>


![站点图现在包括自定义按钮教程的条目](custom-buttons-in-the-datalist-and-repeater-vb/_static/image8.png)

<span data-ttu-id="fe504-132">**图 4**： 站点图现在包括自定义按钮教程的条目</span><span class="sxs-lookup"><span data-stu-id="fe504-132">**Figure 4**: The Site Map Now Includes the Entry for the Custom Buttons Tutorial</span></span>


## <a name="step-2-adding-the-list-of-categories"></a><span data-ttu-id="fe504-133">步骤 2： 添加类别的列表</span><span class="sxs-lookup"><span data-stu-id="fe504-133">Step 2: Adding the List of Categories</span></span>

<span data-ttu-id="fe504-134">我们需要创建中继器，其中列出了所有类别以及显示的产品 LinkButton 本教程中，单击时，项目符号列表中显示的关联的类别的产品。</span><span class="sxs-lookup"><span data-stu-id="fe504-134">For this tutorial we need to create a Repeater that lists all categories along with a Show Products LinkButton that, when clicked, displays the associated category s products in a bulleted list.</span></span> <span data-ttu-id="fe504-135">让我们来首先创建中继器系统中列出的类别的简单。</span><span class="sxs-lookup"><span data-stu-id="fe504-135">Let s first create a simple Repeater that lists the categories in the system.</span></span> <span data-ttu-id="fe504-136">首先打开`CustomButtons.aspx`页面`CustomButtonsDataListRepeater`文件夹。</span><span class="sxs-lookup"><span data-stu-id="fe504-136">Start by opening the `CustomButtons.aspx` page in the `CustomButtonsDataListRepeater` folder.</span></span> <span data-ttu-id="fe504-137">从工具箱中拖动到设计器和组拖动中继器其`ID`属性`Categories`。</span><span class="sxs-lookup"><span data-stu-id="fe504-137">Drag a Repeater from the Toolbox onto the Designer and set its `ID` property to `Categories`.</span></span> <span data-ttu-id="fe504-138">从转发器 s 智能标记，接下来，创建一个新的数据源控件。</span><span class="sxs-lookup"><span data-stu-id="fe504-138">Next, create a new data source control from the Repeater s smart tag.</span></span> <span data-ttu-id="fe504-139">具体而言，创建一个名为的新 ObjectDataSource 控件`CategoriesDataSource`选择从其数据`CategoriesBLL`类的`GetCategories()`方法。</span><span class="sxs-lookup"><span data-stu-id="fe504-139">Specifically, create a new ObjectDataSource control named `CategoriesDataSource` that selects its data from the `CategoriesBLL` class s `GetCategories()` method.</span></span>


<span data-ttu-id="fe504-140">[![配置对象数据源以使用 CategoriesBLL 类的 GetCategories() 方法](custom-buttons-in-the-datalist-and-repeater-vb/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="fe504-140">[![Configure the ObjectDataSource to Use the CategoriesBLL Class s GetCategories() Method](custom-buttons-in-the-datalist-and-repeater-vb/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image9.png)</span></span>

<span data-ttu-id="fe504-141">**图 5**： 配置使用 ObjectDataSource`CategoriesBLL`类 s`GetCategories()`方法 ([单击以查看实际尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="fe504-141">**Figure 5**: Configure the ObjectDataSource to Use the `CategoriesBLL` Class s `GetCategories()` Method ([Click to view full-size image](custom-buttons-in-the-datalist-and-repeater-vb/_static/image11.png))</span></span>


<span data-ttu-id="fe504-142">与 Visual Studio 将为其创建默认的 DataList 控件不同`ItemTemplate`基于数据源，中继器的模板必须手动定义。</span><span class="sxs-lookup"><span data-stu-id="fe504-142">Unlike the DataList control, for which Visual Studio creates a default `ItemTemplate` based on the data source, the Repeater s templates must be manually defined.</span></span> <span data-ttu-id="fe504-143">此外，必须创建并以声明方式编辑转发器的模板 （即，在该处 s 没有编辑的模板选项中继器 s 智能标记中）。</span><span class="sxs-lookup"><span data-stu-id="fe504-143">Furthermore, the Repeater s templates must be created and edited declaratively (that is, there s no Edit Templates option in the Repeater s smart tag).</span></span>

<span data-ttu-id="fe504-144">单击左下角的源选项卡上，然后添加`ItemTemplate`显示中的类别的名称`<h3>`元素和段落中的其描述标记; 包括`SeparatorTemplate`显示水平规则 (`<hr />`) 之间类别。</span><span class="sxs-lookup"><span data-stu-id="fe504-144">Click on the Source tab in the bottom left corner and add an `ItemTemplate` that displays the category s name in an `<h3>` element and its description in a paragraph tag; include a `SeparatorTemplate` that displays a horizontal rule (`<hr />`) between each category.</span></span> <span data-ttu-id="fe504-145">此外将添加与 LinkButton 其`Text`属性设置为显示产品。</span><span class="sxs-lookup"><span data-stu-id="fe504-145">Also add a LinkButton with its `Text` property set to Show Products.</span></span> <span data-ttu-id="fe504-146">完成这些步骤后，你页面 s 声明性标记应如下所示：</span><span class="sxs-lookup"><span data-stu-id="fe504-146">After completing these steps, your page s declarative markup should look like the following:</span></span>


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample2.aspx)]

<span data-ttu-id="fe504-147">图 6 显示的页时查看通过浏览器。</span><span class="sxs-lookup"><span data-stu-id="fe504-147">Figure 6 shows the page when viewed through a browser.</span></span> <span data-ttu-id="fe504-148">列出每个类别名称和描述。</span><span class="sxs-lookup"><span data-stu-id="fe504-148">Each category name and description is listed.</span></span> <span data-ttu-id="fe504-149">显示产品按钮，单击时，会导致回发，但不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="fe504-149">The Show Products button, when clicked, causes a postback but does not yet perform any action.</span></span>


<span data-ttu-id="fe504-150">[![每个类别名称和说明显示，并显示产品 LinkButton](custom-buttons-in-the-datalist-and-repeater-vb/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="fe504-150">[![Each Category s Name and Description is Displayed, Along with a Show Products LinkButton](custom-buttons-in-the-datalist-and-repeater-vb/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image12.png)</span></span>

<span data-ttu-id="fe504-151">**图 6**： 每个类别的名称和描述显示，并显示产品 LinkButton ([单击以查看实际尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="fe504-151">**Figure 6**: Each Category s Name and Description is Displayed, Along with a Show Products LinkButton ([Click to view full-size image](custom-buttons-in-the-datalist-and-repeater-vb/_static/image14.png))</span></span>


## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a><span data-ttu-id="fe504-152">执行服务器端逻辑时显示产品 LinkButton 单击步骤 3:</span><span class="sxs-lookup"><span data-stu-id="fe504-152">Step 3: Executing Server-Side Logic When the Show Products LinkButton is Clicked</span></span>

<span data-ttu-id="fe504-153">单击按钮、 LinkButton 或 DataList 或转发器中的模板内的 ImageButton 后，每当产生的回发和 DataList 或转发器的`ItemCommand`事件激发。</span><span class="sxs-lookup"><span data-stu-id="fe504-153">Anytime a Button, LinkButton, or ImageButton within a template in a DataList or Repeater is clicked, a postback occurs and the DataList or Repeater s `ItemCommand` event fires.</span></span> <span data-ttu-id="fe504-154">除了`ItemCommand`事件，控制可能也会引发其他、 更具针对性的事件，如果 DataList 按钮 s`CommandName`属性设置为的一个保留的字符串 （删除，编辑、 取消、 更新或选择），但`ItemCommand`事件是*始终*激发。</span><span class="sxs-lookup"><span data-stu-id="fe504-154">In addition to the `ItemCommand` event, the DataList control may also raise another, more specific event if the button s `CommandName` property is set to one of the reserved strings ( Delete, Edit, Cancel, Update, or Select ), but the `ItemCommand` event is *always* fired.</span></span>

<span data-ttu-id="fe504-155">DataList 或转发器中单击按钮时，通常我们需要 （如传递 （在这种情况，可能有多个在控件中，如这两个的编辑按钮和删除按钮） 时单击的按钮和可能的一些其他信息主键值其按钮被单击的项）。</span><span class="sxs-lookup"><span data-stu-id="fe504-155">When a button is clicked within a DataList or Repeater, oftentimes we need to pass along which button was clicked (in the case that there may be multiple buttons within the control, such as both an Edit and Delete button) and perhaps some additional information (such as the primary key value of the item whose button was clicked).</span></span> <span data-ttu-id="fe504-156">按钮、 LinkButton 和 ImageButton 提供两个属性，其值传递给`ItemCommand`事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="fe504-156">The Button, LinkButton, and ImageButton provide two properties whose values are passed to the `ItemCommand` event handler:</span></span>

- <span data-ttu-id="fe504-157">`CommandName`通常用于标识在模板中的每个按钮的字符串</span><span class="sxs-lookup"><span data-stu-id="fe504-157">`CommandName` a string typically used to identify each button in the template</span></span>
- <span data-ttu-id="fe504-158">`CommandArgument`通常用来保存某些数据字段，如的主键值的值</span><span class="sxs-lookup"><span data-stu-id="fe504-158">`CommandArgument` commonly used to hold the value of some data field, such as the primary key value</span></span>

<span data-ttu-id="fe504-159">对于此示例中，设置 LinkButton s `CommandName` ShowProducts 和绑定的当前记录 s 主键值的属性`CategoryID`到`CommandArgument`属性使用的数据绑定语法`CategoryArgument='<%# Eval("CategoryID") %>'`。</span><span class="sxs-lookup"><span data-stu-id="fe504-159">For this example, set the LinkButton s `CommandName` property to ShowProducts and bind the current record s primary key value `CategoryID` to the `CommandArgument` property using the databinding syntax `CategoryArgument='<%# Eval("CategoryID") %>'`.</span></span> <span data-ttu-id="fe504-160">指定这两个属性后, LinkButton s 声明性语法应如下所示：</span><span class="sxs-lookup"><span data-stu-id="fe504-160">After specifying these two properties, the LinkButton s declarative syntax should look like the following:</span></span>


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample3.aspx)]

<span data-ttu-id="fe504-161">当单击该按钮，产生的回发和 DataList 或转发器的`ItemCommand`事件激发。</span><span class="sxs-lookup"><span data-stu-id="fe504-161">When the button is clicked, a postback occurs and the DataList or Repeater s `ItemCommand` event fires.</span></span> <span data-ttu-id="fe504-162">事件处理程序传递按钮 s`CommandName`和`CommandArgument`值。</span><span class="sxs-lookup"><span data-stu-id="fe504-162">The event handler is passed the button s `CommandName` and `CommandArgument` values.</span></span>

<span data-ttu-id="fe504-163">为转发器 s 创建事件处理程序`ItemCommand`事件并记下第二个参数传递到事件处理程序 (名为`e`)。</span><span class="sxs-lookup"><span data-stu-id="fe504-163">Create an event handler for the Repeater s `ItemCommand` event and note the second parameter passed into the event handler (named `e`).</span></span> <span data-ttu-id="fe504-164">此第二个参数属于类型[ `RepeaterCommandEventArgs` ](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx)并具有以下四个属性：</span><span class="sxs-lookup"><span data-stu-id="fe504-164">This second parameter is of type [`RepeaterCommandEventArgs`](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx) and has the following four properties:</span></span>

- <span data-ttu-id="fe504-165">`CommandArgument`值被单击的按钮的`CommandArgument`属性</span><span class="sxs-lookup"><span data-stu-id="fe504-165">`CommandArgument` the value of the clicked button s `CommandArgument` property</span></span>
- <span data-ttu-id="fe504-166">`CommandName`按钮的值`CommandName`属性</span><span class="sxs-lookup"><span data-stu-id="fe504-166">`CommandName` the value of the button s `CommandName` property</span></span>
- <span data-ttu-id="fe504-167">`CommandSource`对被单击的按钮控件的引用</span><span class="sxs-lookup"><span data-stu-id="fe504-167">`CommandSource` a reference to the button control that was clicked</span></span>
- <span data-ttu-id="fe504-168">`Item`对引用[ `RepeaterItem` ](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.repeateritem.aspx)包含被单击的按钮; 绑定到中继器每个记录显示为`RepeaterItem`</span><span class="sxs-lookup"><span data-stu-id="fe504-168">`Item` a reference to the [`RepeaterItem`](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.repeateritem.aspx) that contains the button that was clicked; each record bound to the Repeater is manifested as a `RepeaterItem`</span></span>

<span data-ttu-id="fe504-169">由于所选类别 s`CategoryID`通过传入`CommandArgument`属性，我们可以获取与所选类别中关联的产品集`ItemCommand`事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="fe504-169">Since the selected category s `CategoryID` is passed in via the `CommandArgument` property, we can get the set of products associated with the selected category in the `ItemCommand` event handler.</span></span> <span data-ttu-id="fe504-170">然后，这些产品可以绑定到中的如何控件`ItemTemplate`(哪些我们遇到有待添加)。</span><span class="sxs-lookup"><span data-stu-id="fe504-170">These products can then be bound to a BulletedList control in the `ItemTemplate` (which we ve yet to add).</span></span> <span data-ttu-id="fe504-171">所有保持，，然后是添加如何，都引用在`ItemCommand`事件处理程序，并将绑定到它的一套所选类别，在步骤 4 中，我们将介绍的产品。</span><span class="sxs-lookup"><span data-stu-id="fe504-171">All that remains, then, is to add the BulletedList, reference it in the `ItemCommand` event handler, and bind to it the set of products for the selected category, which we'll tackle in Step 4.</span></span>

> [!NOTE]
> <span data-ttu-id="fe504-172">DataList s`ItemCommand`事件处理程序传递的类型对象[ `DataListCommandEventArgs` ](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx)，它提供与相同的四个属性`RepeaterCommandEventArgs`类。</span><span class="sxs-lookup"><span data-stu-id="fe504-172">The DataList s `ItemCommand` event handler is passed an object of type [`DataListCommandEventArgs`](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx), which offers the same four properties as the `RepeaterCommandEventArgs` class.</span></span>


## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a><span data-ttu-id="fe504-173">步骤 4： 在项目符号列表中显示所选的类别的产品</span><span class="sxs-lookup"><span data-stu-id="fe504-173">Step 4: Displaying the Selected Category s Products in a Bulleted List</span></span>

<span data-ttu-id="fe504-174">所选的类别的产品可能显示在转发器的`ItemTemplate`使用任意数量的控件。</span><span class="sxs-lookup"><span data-stu-id="fe504-174">The selected category s products can be displayed within the Repeater s `ItemTemplate` using any number of controls.</span></span> <span data-ttu-id="fe504-175">我们无法添加另一个嵌套中继器、 DataList、 DropDownList、 GridView，等等。</span><span class="sxs-lookup"><span data-stu-id="fe504-175">We could add another nested Repeater, a DataList, a DropDownList, a GridView, and so on.</span></span> <span data-ttu-id="fe504-176">由于我们想要为项目符号列表中显示的产品，不过，我们将使用如何控制。</span><span class="sxs-lookup"><span data-stu-id="fe504-176">Since we want to display the products as a bulleted list, though, we'll use the BulletedList control.</span></span> <span data-ttu-id="fe504-177">返回到`CustomButtons.aspx`页上 s 声明性标记，如何将控件添加到`ItemTemplate`后显示产品 LinkButton。</span><span class="sxs-lookup"><span data-stu-id="fe504-177">Returning to the `CustomButtons.aspx` page s declarative markup, add a BulletedList control to the `ItemTemplate` after the Show Products LinkButton.</span></span> <span data-ttu-id="fe504-178">设置 BulletedLists s`ID`到`ProductsInCategory`。</span><span class="sxs-lookup"><span data-stu-id="fe504-178">Set the BulletedLists s `ID` to `ProductsInCategory`.</span></span> <span data-ttu-id="fe504-179">如何显示通过指定数据字段的值`DataTextField`属性; 因为此控件将有产品信息绑定到它时，请设置`DataTextField`属性`ProductName`。</span><span class="sxs-lookup"><span data-stu-id="fe504-179">The BulletedList displays the value of the data field specified via the `DataTextField` property; since this control will have product information bound to it, set the `DataTextField` property to `ProductName`.</span></span>


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample4.aspx)]

<span data-ttu-id="fe504-180">在`ItemCommand`事件处理程序中，引用此控件使用`e.Item.FindControl("ProductsInCategory")`并将其绑定到与所选类别关联的产品集。</span><span class="sxs-lookup"><span data-stu-id="fe504-180">In the `ItemCommand` event handler, reference this control using `e.Item.FindControl("ProductsInCategory")` and bind it to the set of products associated with the selected category.</span></span>


[!code-vb[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample5.vb)]

<span data-ttu-id="fe504-181">在执行中的任何操作之前`ItemCommand`事件处理程序，它首先检查传入的值比较明智的做法 s `CommandName`。</span><span class="sxs-lookup"><span data-stu-id="fe504-181">Before performing any action in the `ItemCommand` event handler, it s prudent to first check the value of the incoming `CommandName`.</span></span> <span data-ttu-id="fe504-182">由于`ItemCommand`事件处理程序，则会激发*任何*单击按钮时，如果模板使用中有多个按钮`CommandName`值以便辨别要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="fe504-182">Since the `ItemCommand` event handler fires when *any* button is clicked, if there are multiple buttons in the template use the `CommandName` value to discern what action to take.</span></span> <span data-ttu-id="fe504-183">检查`CommandName`此处毫无意义，因为只有一个按钮，但它是一个好习惯到窗体。</span><span class="sxs-lookup"><span data-stu-id="fe504-183">Checking the `CommandName` here is moot, since we only have a single button, but it is a good habit to form.</span></span> <span data-ttu-id="fe504-184">接下来，`CategoryID`检索所选类别的从`CommandArgument`属性。</span><span class="sxs-lookup"><span data-stu-id="fe504-184">Next, the `CategoryID` of the selected category is retrieved from the `CommandArgument` property.</span></span> <span data-ttu-id="fe504-185">在模板中的如何控件然后引用并绑定到的结果`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。</span><span class="sxs-lookup"><span data-stu-id="fe504-185">The BulletedList control in the template is then referenced and bound to the results of the `ProductsBLL` class s `GetProductsByCategoryID(categoryID)` method.</span></span>

<span data-ttu-id="fe504-186">在前面的教程，如使用内 DataList 按钮[概述的编辑和删除数据中 DataList](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)，我们确定通过给定项的主键值`DataKeys`集合。</span><span class="sxs-lookup"><span data-stu-id="fe504-186">In previous tutorials that used the buttons within a DataList, such as [An Overview of Editing and Deleting Data in the DataList](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md), we determined the primary key value of a given item via the `DataKeys` collection.</span></span> <span data-ttu-id="fe504-187">虽然此方法适用于 DataList，中继器没有`DataKeys`属性。</span><span class="sxs-lookup"><span data-stu-id="fe504-187">While this approach works well with the DataList, the Repeater does not have a `DataKeys` property.</span></span> <span data-ttu-id="fe504-188">相反，我们必须使用另一种方法提供的主键值，如通过按钮的`CommandArgument`属性或将主键值分配到隐藏标签 Web 控件模板内，并读取其值进来`ItemCommand`事件处理程序使用`e.Item.FindControl("LabelID")`。</span><span class="sxs-lookup"><span data-stu-id="fe504-188">Instead, we must use an alternative approach for supplying the primary key value, such as through the button s `CommandArgument` property or by assigning the primary key value to a hidden Label Web control within the template and reading its value back in the `ItemCommand` event handler using `e.Item.FindControl("LabelID")`.</span></span>

<span data-ttu-id="fe504-189">完成后`ItemCommand`事件处理程序，需要一段时间来测试此页在浏览器。</span><span class="sxs-lookup"><span data-stu-id="fe504-189">After completing the `ItemCommand` event handler, take a moment to test out this page in a browser.</span></span> <span data-ttu-id="fe504-190">如图 7 所示，单击显示产品链接导致回发并中如何显示所选类别的产品。</span><span class="sxs-lookup"><span data-stu-id="fe504-190">As Figure 7 shows, clicking the Show Products link causes a postback and displays the products for the selected category in a BulletedList.</span></span> <span data-ttu-id="fe504-191">此外，请注意，此产品信息将保持，即使在单击其他类别显示产品链接。</span><span class="sxs-lookup"><span data-stu-id="fe504-191">Furthermore, note that this product information remains, even if other categories Show Products links are clicked.</span></span>

> [!NOTE]
> <span data-ttu-id="fe504-192">如果你想要修改此报表的行为，这样只有一个类别的产品列出一次，只需设置如何控制 s`EnableViewState`属性`False`。</span><span class="sxs-lookup"><span data-stu-id="fe504-192">If you want to modify the behavior of this report, such that the only one category s products are listed at a time, simply set the BulletedList control s `EnableViewState` property to `False`.</span></span>


<span data-ttu-id="fe504-193">[![如何用来显示所选分类的产品](custom-buttons-in-the-datalist-and-repeater-vb/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="fe504-193">[![A BulletedList is used to Display the Products of the Selected Category](custom-buttons-in-the-datalist-and-repeater-vb/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image15.png)</span></span>

<span data-ttu-id="fe504-194">**图 7**: 如何用来显示所选分类的产品 ([单击以查看实际尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="fe504-194">**Figure 7**: A BulletedList is used to Display the Products of the Selected Category ([Click to view full-size image](custom-buttons-in-the-datalist-and-repeater-vb/_static/image17.png))</span></span>


## <a name="summary"></a><span data-ttu-id="fe504-195">摘要</span><span class="sxs-lookup"><span data-stu-id="fe504-195">Summary</span></span>

<span data-ttu-id="fe504-196">DataList 和转发器控件可以包含在其模板中任意数量的按钮、 LinkButtons 或 ImageButtons。</span><span class="sxs-lookup"><span data-stu-id="fe504-196">The DataList and Repeater controls can include any number of Buttons, LinkButtons, or ImageButtons within their templates.</span></span> <span data-ttu-id="fe504-197">此类按钮，单击时，会导致回发和引发`ItemCommand`事件。</span><span class="sxs-lookup"><span data-stu-id="fe504-197">Such buttons, when clicked, cause a postback and raise the `ItemCommand` event.</span></span> <span data-ttu-id="fe504-198">若要将自定义服务器端操作相关联与所单击的按钮，创建的事件处理程序`ItemCommand`事件。</span><span class="sxs-lookup"><span data-stu-id="fe504-198">To associate custom server-side action with a button being clicked, create an event handler for the `ItemCommand` event.</span></span> <span data-ttu-id="fe504-199">在此事件处理程序首先检查传入`CommandName`值以确定被单击的按钮。</span><span class="sxs-lookup"><span data-stu-id="fe504-199">In this event handler first check the incoming `CommandName` value to determine which button was clicked.</span></span> <span data-ttu-id="fe504-200">其他信息 （可选） 可以提供通过按钮的`CommandArgument`属性。</span><span class="sxs-lookup"><span data-stu-id="fe504-200">Additional information can optionally be supplied through the button s `CommandArgument` property.</span></span>

<span data-ttu-id="fe504-201">尽情享受编程 ！</span><span class="sxs-lookup"><span data-stu-id="fe504-201">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="fe504-202">关于作者</span><span class="sxs-lookup"><span data-stu-id="fe504-202">About the Author</span></span>

<span data-ttu-id="fe504-203">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七个 ASP/ASP.NET 书籍和的创始人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年使用与 Microsoft Web 技术。</span><span class="sxs-lookup"><span data-stu-id="fe504-203">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="fe504-204">Scott 的作用是作为独立的顾问、 培训师和编写器。</span><span class="sxs-lookup"><span data-stu-id="fe504-204">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="fe504-205">最新书籍是[ *Sam 教授自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="fe504-205">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="fe504-206">他可以达到在[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)或通过他的博客，其中可以找到在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="fe504-206">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="fe504-207">特别感谢</span><span class="sxs-lookup"><span data-stu-id="fe504-207">Special Thanks To</span></span>

<span data-ttu-id="fe504-208">本教程系列已由许多有用的审阅者评审。</span><span class="sxs-lookup"><span data-stu-id="fe504-208">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="fe504-209">本教程中的前导审阅者已 Dennis Patterson。</span><span class="sxs-lookup"><span data-stu-id="fe504-209">Lead reviewer for this tutorial was Dennis Patterson.</span></span> <span data-ttu-id="fe504-210">对感兴趣查看我即将到来的 MSDN 文章？</span><span class="sxs-lookup"><span data-stu-id="fe504-210">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="fe504-211">如果是这样，删除我一行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="fe504-211">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="fe504-212">上一篇</span><span class="sxs-lookup"><span data-stu-id="fe504-212">Previous</span></span>](custom-buttons-in-the-datalist-and-repeater-cs.md)