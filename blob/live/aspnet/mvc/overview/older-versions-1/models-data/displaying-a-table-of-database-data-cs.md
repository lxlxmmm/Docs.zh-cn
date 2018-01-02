---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: "显示表的数据库数据 (C#) |Microsoft 文档"
author: microsoft
description: "在本教程中，我将演示两种方法可以显示一组数据库记录。 我显示以下两种格式的一组数据库记录在 HTML 数据..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 37ea081df2ee26e186669b815a4d769e1976ae9c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="displaying-a-table-of-database-data-c"></a><span data-ttu-id="4d5d7-104">显示表的数据库数据 (C#)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-104">Displaying a Table of Database Data (C#)</span></span>
====================
<span data-ttu-id="4d5d7-105">通过[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="4d5d7-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="4d5d7-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> <span data-ttu-id="4d5d7-107">在本教程中，我将演示两种方法可以显示一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="4d5d7-108">我将介绍两种格式的 HTML 表中的数据库记录的一组方法。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="4d5d7-109">首先，我介绍如何设置格式的视图中直接的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="4d5d7-110">接下来，我演示如何可以充分利用它们，当数据库记录进行格式化。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>


<span data-ttu-id="4d5d7-111">本教程旨在说明如何可以在 ASP.NET MVC 应用程序中显示一个 HTML 表的数据库数据。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="4d5d7-112">首先，你将学习如何使用 Visual Studio 中包含的基架工具来生成自动显示一组记录的视图。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="4d5d7-113">接下来，你将了解如何格式化数据库记录时将用作模板的部分。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="4d5d7-114">创建模型类</span><span class="sxs-lookup"><span data-stu-id="4d5d7-114">Create the Model Classes</span></span>

<span data-ttu-id="4d5d7-115">我们将会显示的电影数据库表中的记录集。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="4d5d7-116">电影数据库表包含以下列：</span><span class="sxs-lookup"><span data-stu-id="4d5d7-116">The Movies database table contains the following columns:</span></span>

<a id="0.3_table01"></a>


| <span data-ttu-id="4d5d7-117">**列名称**</span><span class="sxs-lookup"><span data-stu-id="4d5d7-117">**Column Name**</span></span> | <span data-ttu-id="4d5d7-118">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="4d5d7-118">**Data Type**</span></span> | <span data-ttu-id="4d5d7-119">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="4d5d7-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d5d7-120">Id</span><span class="sxs-lookup"><span data-stu-id="4d5d7-120">Id</span></span> | <span data-ttu-id="4d5d7-121">Int</span><span class="sxs-lookup"><span data-stu-id="4d5d7-121">Int</span></span> | <span data-ttu-id="4d5d7-122">False</span><span class="sxs-lookup"><span data-stu-id="4d5d7-122">False</span></span> |
| <span data-ttu-id="4d5d7-123">标题</span><span class="sxs-lookup"><span data-stu-id="4d5d7-123">Title</span></span> | <span data-ttu-id="4d5d7-124">Nvarchar （200)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-124">Nvarchar(200)</span></span> | <span data-ttu-id="4d5d7-125">False</span><span class="sxs-lookup"><span data-stu-id="4d5d7-125">False</span></span> |
| <span data-ttu-id="4d5d7-126">控制器</span><span class="sxs-lookup"><span data-stu-id="4d5d7-126">Director</span></span> | <span data-ttu-id="4d5d7-127">NVarchar(50)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-127">NVarchar(50)</span></span> | <span data-ttu-id="4d5d7-128">False</span><span class="sxs-lookup"><span data-stu-id="4d5d7-128">False</span></span> |
| <span data-ttu-id="4d5d7-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="4d5d7-129">DateReleased</span></span> | <span data-ttu-id="4d5d7-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="4d5d7-130">DateTime</span></span> | <span data-ttu-id="4d5d7-131">False</span><span class="sxs-lookup"><span data-stu-id="4d5d7-131">False</span></span> |


<span data-ttu-id="4d5d7-132">为了表示我们 ASP.NET MVC 应用程序中的电影表，我们需要创建一个模型类。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="4d5d7-133">在本教程中，我们可以使用 Microsoft 实体框架来创建我们模型的类。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4d5d7-134">在本教程中，我们使用 Microsoft 实体框架。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="4d5d7-135">但是，务必了解你可以使用各种不同的技术来与从 ASP.NET MVC 应用程序包括 LINQ to SQL、 NHibernate 或 ADO.NET 数据库交互。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>


<span data-ttu-id="4d5d7-136">请按照下列步骤以启动实体数据模型向导：</span><span class="sxs-lookup"><span data-stu-id="4d5d7-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="4d5d7-137">右键单击解决方案资源管理器窗口，然后选择菜单选项中的 Models 文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="4d5d7-138">选择**数据**类别，然后选择**ADO.NET 实体数据模型**模板。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="4d5d7-139">将命名的数据模型*MoviesDBModel.edmx*单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="4d5d7-140">单击添加按钮后，则将显示实体数据模型向导 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="4d5d7-141">请按照下列步骤以完成向导：</span><span class="sxs-lookup"><span data-stu-id="4d5d7-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="4d5d7-142">在**选择模型内容**步骤中，选择**从数据库生成**选项。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="4d5d7-143">在**选择你的数据连接**步骤中，使用*MoviesDB.mdf*数据连接和名称*MoviesDBEntities*对于连接设置。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="4d5d7-144">单击**下一步**按钮。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="4d5d7-145">在**选择数据库对象**步骤，展开表节点，选择电影表。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="4d5d7-146">输入的命名空间*模型*单击**完成**按钮。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-146">Enter the namespace *Models* and click the **Finish** button.</span></span>


<span data-ttu-id="4d5d7-147">[![创建 LINQ to SQL 类](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="4d5d7-148">**图 01**： 创建 LINQ to SQL 类 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="4d5d7-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image2.png))</span></span>


<span data-ttu-id="4d5d7-149">完成实体数据模型向导后，将打开实体数据模型设计器。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="4d5d7-150">设计器应显示电影实体 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-150">The Designer should display the Movies entity (see Figure 2).</span></span>


<span data-ttu-id="4d5d7-151">[![实体数据模型设计器](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span></span>

<span data-ttu-id="4d5d7-152">**图 02**: 实体数据模型设计器 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="4d5d7-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image4.png))</span></span>


<span data-ttu-id="4d5d7-153">我们需要进行一次更改，我们继续操作之前。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-153">We need to make one change before we continue.</span></span> <span data-ttu-id="4d5d7-154">实体数据向导生成一个名为的模型类*电影*表示电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="4d5d7-155">因为我们将使用影片类来表示特定电影，我们需要修改的类的名称*电影*而不是*电影*（单数而复数形式）。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="4d5d7-156">双击设计器图面上的类的名称，并将影片中的类的名称更改为影片。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="4d5d7-157">此更改后，单击**保存**按钮 （软盘图标） 生成电影类。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="4d5d7-158">创建电影控制器</span><span class="sxs-lookup"><span data-stu-id="4d5d7-158">Create the Movies Controller</span></span>

<span data-ttu-id="4d5d7-159">现在，我们已表示我们的数据库记录的方式，我们可以创建返回的电影收藏的控制器。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="4d5d7-160">在 Visual Studio 解决方案资源管理器窗口中，右键单击 Controllers 文件夹，然后选择菜单选项**添加、 控制器**（请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>


<span data-ttu-id="4d5d7-161">[![添加控制器菜单](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-161">[![The Add Controller Menu](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span></span>

<span data-ttu-id="4d5d7-162">**图 03**: 添加控制器菜单 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="4d5d7-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image6.png))</span></span>


<span data-ttu-id="4d5d7-163">当**添加控制器**对话框出现时，输入控制器名称 MovieController （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="4d5d7-164">单击**添加**按钮以添加新控制器。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-164">Click the **Add** button to add the new controller.</span></span>


<span data-ttu-id="4d5d7-165">[![添加控制器对话框](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-165">[![The Add Controller dialog](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span></span>

<span data-ttu-id="4d5d7-166">**图 04**: 添加控制器对话框 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="4d5d7-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image8.png))</span></span>


<span data-ttu-id="4d5d7-167">我们需要修改从而使其返回的数据库记录集公开的电影控制器的 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="4d5d7-168">修改控制器，以便它如下所示列出 1 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="4d5d7-169">**列表 1 – Controllers\MovieController.cs**</span><span class="sxs-lookup"><span data-stu-id="4d5d7-169">**Listing 1 – Controllers\MovieController.cs**</span></span>

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

<span data-ttu-id="4d5d7-170">在清单 1 MoviesDBEntities 类用于表示 MoviesDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="4d5d7-171">若要使用此类，你需要导入如下 MvcApplication1.Models 命名空间：</span><span class="sxs-lookup"><span data-stu-id="4d5d7-171">To use this class, you need to import the MvcApplication1.Models namespace like this:</span></span>

<span data-ttu-id="4d5d7-172">使用 MvcApplication1.Models;</span><span class="sxs-lookup"><span data-stu-id="4d5d7-172">using MvcApplication1.Models;</span></span>

<span data-ttu-id="4d5d7-173">表达式*实体。MovieSet.ToList()*返回所有电影的集，从电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-173">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="4d5d7-174">创建视图</span><span class="sxs-lookup"><span data-stu-id="4d5d7-174">Create the View</span></span>

<span data-ttu-id="4d5d7-175">HTML 表中显示一组数据库记录的最简单方法是利用 Visual Studio 提供的基架。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-175">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="4d5d7-176">通过选择菜单选项来生成你的应用程序**生成，生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-176">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="4d5d7-177">必须生成应用程序在打开之前**添加视图**数据类或对话框不会显示在对话框。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-177">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="4d5d7-178">右键单击 index （） 操作，然后选择菜单选项**添加视图**（请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-178">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>


<span data-ttu-id="4d5d7-179">[![添加视图](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-179">[![Adding a view](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span></span>

<span data-ttu-id="4d5d7-180">**图 05**： 添加视图 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="4d5d7-180">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image10.png))</span></span>


<span data-ttu-id="4d5d7-181">在**添加视图**对话框中，选中复选框标记为**创建强类型化视图**。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-181">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="4d5d7-182">选择的电影类**查看数据类**。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-182">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="4d5d7-183">选择*列表*作为**查看内容**（请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-183">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="4d5d7-184">选择这些选项将生成一个强类型的视图，显示影片列表。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-184">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>


<span data-ttu-id="4d5d7-185">[![添加视图对话框](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-185">[![The Add View dialog](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="4d5d7-186">**图 06**: 添加视图对话框 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="4d5d7-186">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image12.png))</span></span>


<span data-ttu-id="4d5d7-187">单击后**添加**按钮，列出 2 中的视图自动生成。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-187">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="4d5d7-188">此视图包含循环访问的电影收藏并显示一部电影的属性的每个所需的代码。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-188">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="4d5d7-189">**列出 2 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="4d5d7-189">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

<span data-ttu-id="4d5d7-190">你可以通过选择菜单选项来运行该应用程序**调试、 启动调试**（或按 F5 键）。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-190">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="4d5d7-191">运行应用程序将启动 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-191">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="4d5d7-192">如果您导航到 /Movie URL，然后你将看到图 7 中的页。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-192">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>


<span data-ttu-id="4d5d7-193">[![表的电影](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-193">[![A table of movies](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span></span>

<span data-ttu-id="4d5d7-194">**图 07**： 电影的表 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="4d5d7-194">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image14.png))</span></span>


<span data-ttu-id="4d5d7-195">如果你不喜欢有关图 7 中的数据库记录的网格的外观的任何信息则可以只需修改索引视图。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-195">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="4d5d7-196">例如，您可以更改*DateReleased*标头到*发布日期*通过修改索引视图。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-196">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="4d5d7-197">使用部分创建一个模板</span><span class="sxs-lookup"><span data-stu-id="4d5d7-197">Create a Template with a Partial</span></span>

<span data-ttu-id="4d5d7-198">当视图获取过于复杂时，它是启动视图拆分为它们的一个好办法。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-198">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="4d5d7-199">使用它们可以更轻松地理解和维护你的视图。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-199">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="4d5d7-200">我们将创建一个分部，我们可以使用作为模板来设置每个电影数据库记录的格式。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-200">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="4d5d7-201">请按照以下步骤创建分部操作：</span><span class="sxs-lookup"><span data-stu-id="4d5d7-201">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="4d5d7-202">右键单击 Views\Movie 文件夹然后选择菜单选项**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-202">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="4d5d7-203">选中复选框标记为*创建了分部视图 (.ascx)*。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-203">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="4d5d7-204">命名分部*MovieTemplate*。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-204">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="4d5d7-205">选中复选框标记为**创建强类型化视图**。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-205">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="4d5d7-206">选择部电影作为*查看数据类*。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-206">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="4d5d7-207">选择作为空*查看内容*。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-207">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="4d5d7-208">单击**添加**按钮将部分添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-208">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="4d5d7-209">完成这些步骤后，修改部分 MovieTemplate 如下所示列出 3。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-209">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="4d5d7-210">**列出 3 – Views\Movie\MovieTemplate.ascx**</span><span class="sxs-lookup"><span data-stu-id="4d5d7-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

<span data-ttu-id="4d5d7-211">列出 3 中的部分包含记录的单个行的模板。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-211">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="4d5d7-212">已修改的索引视图，列出 4 中使用部分 MovieTemplate。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-212">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="4d5d7-213">**列出 4 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="4d5d7-213">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

<span data-ttu-id="4d5d7-214">该视图列出 4 中的包含的 foreach 循环中循环访问所有影片。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-214">The view in Listing 4 contains a foreach loop that iterates through all of the movies.</span></span> <span data-ttu-id="4d5d7-215">为每个的电影，部分 MovieTemplate 用于格式化影片。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-215">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="4d5d7-216">MovieTemplate 呈现通过调用 RenderPartial() 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-216">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="4d5d7-217">已修改的索引视图呈现非常同一个 HTML 表的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-217">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="4d5d7-218">但是，该视图进行了极大地简化。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-218">However, the view has been greatly simplified.</span></span>


<span data-ttu-id="4d5d7-219">RenderPartial() 方法是不同于大多数其他帮助器方法，因为它不返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-219">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="4d5d7-220">因此，必须调用 RenderPartial() 方法使用&lt;%html.renderpartial(); %&gt;而不是&lt;%= Html.RenderPartial(); %&gt;。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-220">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial(); %&gt; instead of &lt;%= Html.RenderPartial(); %&gt;.</span></span>


## <a name="summary"></a><span data-ttu-id="4d5d7-221">摘要</span><span class="sxs-lookup"><span data-stu-id="4d5d7-221">Summary</span></span>

<span data-ttu-id="4d5d7-222">本教程的目的是说明如何可以在 HTML 表中显示一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-222">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="4d5d7-223">首先，您学习了如何通过利用 Microsoft 实体框架的控制器操作返回一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-223">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="4d5d7-224">接下来，您学习了如何使用 Visual Studio 基架以生成一个视图，自动显示项的集合。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-224">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="4d5d7-225">最后，您学习了如何通过利用部分的简化视图。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-225">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="4d5d7-226">您学习了如何将用作模板的部分，以便你可以设置每个数据库记录的格式。</span><span class="sxs-lookup"><span data-stu-id="4d5d7-226">You learned how to use a partial as a template so that you can format each database record.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="4d5d7-227">[上一页](creating-model-classes-with-linq-to-sql-cs.md)
[下一页](performing-simple-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="4d5d7-227">[Previous](creating-model-classes-with-linq-to-sql-cs.md)
[Next](performing-simple-validation-cs.md)</span></span>