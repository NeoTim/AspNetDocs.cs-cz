---
title: Přizpůsobení modelu identity v ASP.NET Core
author: ajcvickers
description: Tento článek popisuje, jak přizpůsobit základní datový model Entity Framework Core pro ASP.NET Core Identity.
ms.author: avickers
ms.date: 09/24/2018
uid: security/authentication/customize_identity_model
ms.openlocfilehash: 90c867eeac0e64bfe77cc7a829d61e831a2fb8e1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066046"
---
# <a name="identity-model-customization-in-aspnet-core"></a><span data-ttu-id="ca627-103">Přizpůsobení modelu identity v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ca627-103">Identity model customization in ASP.NET Core</span></span>

<span data-ttu-id="ca627-104">Podle [podle Arthur Vickerse](https://github.com/ajcvickers)</span><span class="sxs-lookup"><span data-stu-id="ca627-104">By [Arthur Vickers](https://github.com/ajcvickers)</span></span>

<span data-ttu-id="ca627-105">ASP.NET Core Identity poskytuje rozhraní pro správu a ukládání uživatelských účtů v aplikacích ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="ca627-105">ASP.NET Core Identity provides a framework for managing and storing user accounts in ASP.NET Core apps.</span></span> <span data-ttu-id="ca627-106">Identita je přidána do projektu při **jednotlivé uživatelské účty** je zvolen jako mechanismus ověřování.</span><span class="sxs-lookup"><span data-stu-id="ca627-106">Identity is added to your project when **Individual User Accounts** is selected as the authentication mechanism.</span></span> <span data-ttu-id="ca627-107">Ve výchozím nastavení, Identity využívá sady Entity Framework (EF) základní datový model.</span><span class="sxs-lookup"><span data-stu-id="ca627-107">By default, Identity makes use of an Entity Framework (EF) Core data model.</span></span> <span data-ttu-id="ca627-108">Tento článek popisuje, jak přizpůsobit modelem Identity.</span><span class="sxs-lookup"><span data-stu-id="ca627-108">This article describes how to customize the Identity model.</span></span>

## <a name="identity-and-ef-core-migrations"></a><span data-ttu-id="ca627-109">Identity a migrace EF Core</span><span class="sxs-lookup"><span data-stu-id="ca627-109">Identity and EF Core Migrations</span></span>

<span data-ttu-id="ca627-110">Před prozkoumání modelu, je užitečné k pochopení fungování Identity s [migrace EF Core](/ef/core/managing-schemas/migrations/) k vytvoření a aktualizaci databáze.</span><span class="sxs-lookup"><span data-stu-id="ca627-110">Before examining the model, it's useful to understand how Identity works with [EF Core Migrations](/ef/core/managing-schemas/migrations/) to create and update a database.</span></span> <span data-ttu-id="ca627-111">Proces je na nejvyšší úrovni:</span><span class="sxs-lookup"><span data-stu-id="ca627-111">At the top level, the process is:</span></span>

1. <span data-ttu-id="ca627-112">Definovat nebo aktualizovat [datového modelu v kódu](/ef/core/modeling/).</span><span class="sxs-lookup"><span data-stu-id="ca627-112">Define or update a [data model in code](/ef/core/modeling/).</span></span>
1. <span data-ttu-id="ca627-113">Přidejte migraci na tomto modelu se převedou změny, které mohou být použity k databázi.</span><span class="sxs-lookup"><span data-stu-id="ca627-113">Add a Migration to translate this model into changes that can be applied to the database.</span></span>
1. <span data-ttu-id="ca627-114">Zkontrolujte, že migrace správně představuje vaše záměry.</span><span class="sxs-lookup"><span data-stu-id="ca627-114">Check that the Migration correctly represents your intentions.</span></span>
1. <span data-ttu-id="ca627-115">Použití migrace k aktualizaci databáze byly synchronizované s modelem.</span><span class="sxs-lookup"><span data-stu-id="ca627-115">Apply the Migration to update the database to be in sync with the model.</span></span>
1. <span data-ttu-id="ca627-116">Opakujte kroky 1 až 4 dále upřesnit modelu a zachovat databázi synchronizované.</span><span class="sxs-lookup"><span data-stu-id="ca627-116">Repeat steps 1 through 4 to further refine the model and keep the database in sync.</span></span>

<span data-ttu-id="ca627-117">Přidat a použití migrace, použijte jednu z následujících postupů:</span><span class="sxs-lookup"><span data-stu-id="ca627-117">Use one of the following approaches to add and apply Migrations:</span></span>

* <span data-ttu-id="ca627-118">**Konzola správce balíčků** okno (PMC) Pokud pomocí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca627-118">The **Package Manager Console** (PMC) window if using Visual Studio.</span></span> <span data-ttu-id="ca627-119">Další informace najdete v tématu [EF Core PMC tools](/ef/core/miscellaneous/cli/powershell).</span><span class="sxs-lookup"><span data-stu-id="ca627-119">For more information, see [EF Core PMC tools](/ef/core/miscellaneous/cli/powershell).</span></span>
* <span data-ttu-id="ca627-120">.NET Core CLI Pokud pomocí příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="ca627-120">The .NET Core CLI if using the command line.</span></span> <span data-ttu-id="ca627-121">Další informace najdete v tématu [nástroje příkazového řádku EF Core .NET](/ef/core/miscellaneous/cli/dotnet).</span><span class="sxs-lookup"><span data-stu-id="ca627-121">For more information, see [EF Core .NET command line tools](/ef/core/miscellaneous/cli/dotnet).</span></span>
* <span data-ttu-id="ca627-122">Kliknutím **migrace použít** tlačítko na chybovou stránku při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="ca627-122">Clicking the **Apply Migrations** button on the error page when the app is run.</span></span>

<span data-ttu-id="ca627-123">ASP.NET Core má dobu vývoje chybová stránka.</span><span class="sxs-lookup"><span data-stu-id="ca627-123">ASP.NET Core has a development-time error page handler.</span></span> <span data-ttu-id="ca627-124">Obslužná rutina provést migrace při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="ca627-124">The handler can apply migrations when the app is run.</span></span> <span data-ttu-id="ca627-125">Pro produkční aplikace, často je vhodné generovat SQL skripty z migrace a nasazení změn databází jako součást řízené nasazení aplikace a databáze.</span><span class="sxs-lookup"><span data-stu-id="ca627-125">For production apps, it's often more appropriate to generate SQL scripts from the migrations and deploy database changes as part of a controlled app and database deployment.</span></span>

<span data-ttu-id="ca627-126">Když se vytvoří nová aplikace využívající identitu, kroky 1 a 2 výše již dokončena.</span><span class="sxs-lookup"><span data-stu-id="ca627-126">When a new app using Identity is created, steps 1 and 2 above have already been completed.</span></span> <span data-ttu-id="ca627-127">To znamená že původního datového modelu již existuje, a počáteční migraci se přidal do projektu.</span><span class="sxs-lookup"><span data-stu-id="ca627-127">That is, the initial data model already exists, and the initial migration has been added to the project.</span></span> <span data-ttu-id="ca627-128">Počáteční migraci stále musí být použita pro databázi.</span><span class="sxs-lookup"><span data-stu-id="ca627-128">The initial migration still needs to be applied to the database.</span></span> <span data-ttu-id="ca627-129">Počáteční migraci můžete použít některou z následujících postupů:</span><span class="sxs-lookup"><span data-stu-id="ca627-129">The initial migration can be applied via one of the following approaches:</span></span>

* <span data-ttu-id="ca627-130">Spustit `Update-Database` v konzole PMC.</span><span class="sxs-lookup"><span data-stu-id="ca627-130">Run `Update-Database` in PMC.</span></span>
* <span data-ttu-id="ca627-131">Spustit `dotnet ef database update` v příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="ca627-131">Run `dotnet ef database update` in a command shell.</span></span>
* <span data-ttu-id="ca627-132">Klikněte na tlačítko **migrace použít** tlačítko na chybovou stránku při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="ca627-132">Click the **Apply Migrations** button on the error page when the app is run.</span></span>

<span data-ttu-id="ca627-133">Zopakujte předchozí kroky, jakmile jsou provedeny změny modelu.</span><span class="sxs-lookup"><span data-stu-id="ca627-133">Repeat the preceding steps as changes are made to the model.</span></span>

## <a name="the-identity-model"></a><span data-ttu-id="ca627-134">Modelem Identity</span><span class="sxs-lookup"><span data-stu-id="ca627-134">The Identity model</span></span>

### <a name="entity-types"></a><span data-ttu-id="ca627-135">Typy entit</span><span class="sxs-lookup"><span data-stu-id="ca627-135">Entity types</span></span>

<span data-ttu-id="ca627-136">Identity model se skládá z následujících typů entit.</span><span class="sxs-lookup"><span data-stu-id="ca627-136">The Identity model consists of the following entity types.</span></span>

|<span data-ttu-id="ca627-137">Typ entity</span><span class="sxs-lookup"><span data-stu-id="ca627-137">Entity type</span></span>|<span data-ttu-id="ca627-138">Popis</span><span class="sxs-lookup"><span data-stu-id="ca627-138">Description</span></span>                                                  |
|-----------|-------------------------------------------------------------|
|`User`     |<span data-ttu-id="ca627-139">Představuje uživatele.</span><span class="sxs-lookup"><span data-stu-id="ca627-139">Represents the user.</span></span>                                         |
|`Role`     |<span data-ttu-id="ca627-140">Představuje roli.</span><span class="sxs-lookup"><span data-stu-id="ca627-140">Represents a role.</span></span>                                           |
|`UserClaim`|<span data-ttu-id="ca627-141">Reprezentuje deklaraci identity, který má uživatel.</span><span class="sxs-lookup"><span data-stu-id="ca627-141">Represents a claim that a user possesses.</span></span>                    |
|`UserToken`|<span data-ttu-id="ca627-142">Představuje ověřovací token pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="ca627-142">Represents an authentication token for a user.</span></span>               |
|`UserLogin`|<span data-ttu-id="ca627-143">Přidruží přihlášení uživatele.</span><span class="sxs-lookup"><span data-stu-id="ca627-143">Associates a user with a login.</span></span>                              |
|`RoleClaim`|<span data-ttu-id="ca627-144">Reprezentuje deklaraci identity, které je udělen pro všechny uživatele v rámci role.</span><span class="sxs-lookup"><span data-stu-id="ca627-144">Represents a claim that's granted to all users within a role.</span></span>|
|`UserRole` |<span data-ttu-id="ca627-145">Spojení entit, které přidružuje uživatelů a rolí.</span><span class="sxs-lookup"><span data-stu-id="ca627-145">A join entity that associates users and roles.</span></span>               |

### <a name="entity-type-relationships"></a><span data-ttu-id="ca627-146">Entitu typu vztahy</span><span class="sxs-lookup"><span data-stu-id="ca627-146">Entity type relationships</span></span>

<span data-ttu-id="ca627-147">[Typy entit](#entity-types) se vztahují k sobě navzájem následujícími způsoby:</span><span class="sxs-lookup"><span data-stu-id="ca627-147">The [entity types](#entity-types) are related to each other in the following ways:</span></span>

* <span data-ttu-id="ca627-148">Každý `User` může mít mnoho `UserClaims`.</span><span class="sxs-lookup"><span data-stu-id="ca627-148">Each `User` can have many `UserClaims`.</span></span>
* <span data-ttu-id="ca627-149">Každý `User` může mít mnoho `UserLogins`.</span><span class="sxs-lookup"><span data-stu-id="ca627-149">Each `User` can have many `UserLogins`.</span></span>
* <span data-ttu-id="ca627-150">Každý `User` může mít mnoho `UserTokens`.</span><span class="sxs-lookup"><span data-stu-id="ca627-150">Each `User` can have many `UserTokens`.</span></span>
* <span data-ttu-id="ca627-151">Každý `Role` může mít mnoho přidružené `RoleClaims`.</span><span class="sxs-lookup"><span data-stu-id="ca627-151">Each `Role` can have many associated `RoleClaims`.</span></span>
* <span data-ttu-id="ca627-152">Každý `User` může mít mnoho přidružené `Roles`a každý `Role` můžou být spojené s mnoha `Users`.</span><span class="sxs-lookup"><span data-stu-id="ca627-152">Each `User` can have many associated `Roles`, and each `Role` can be associated with many `Users`.</span></span> <span data-ttu-id="ca627-153">Toto je vztah many-to-many, který vyžaduje připojení k tabulku v databázi.</span><span class="sxs-lookup"><span data-stu-id="ca627-153">This is a many-to-many relationship that requires a join table in the database.</span></span> <span data-ttu-id="ca627-154">Tabulky spojení reprezentována `UserRole` entity.</span><span class="sxs-lookup"><span data-stu-id="ca627-154">The join table is represented by the `UserRole` entity.</span></span>

### <a name="default-model-configuration"></a><span data-ttu-id="ca627-155">Výchozí konfigurace modelu</span><span class="sxs-lookup"><span data-stu-id="ca627-155">Default model configuration</span></span>

<span data-ttu-id="ca627-156">Identity definuje mnoho *třídy kontextu* , která dědí z <xref:Microsoft.EntityFrameworkCore.DbContext> ke konfiguraci a použití modelu.</span><span class="sxs-lookup"><span data-stu-id="ca627-156">Identity defines many *context classes* that inherit from <xref:Microsoft.EntityFrameworkCore.DbContext> to configure and use the model.</span></span> <span data-ttu-id="ca627-157">Tato konfigurace se provádí pomocí [EF Core kód první Fluent API](/ef/core/modeling/) v <xref:Microsoft.EntityFrameworkCore.DbContext.OnModelCreating*> metody třídy kontextu.</span><span class="sxs-lookup"><span data-stu-id="ca627-157">This configuration is done using the [EF Core Code First Fluent API](/ef/core/modeling/) in the <xref:Microsoft.EntityFrameworkCore.DbContext.OnModelCreating*> method of the context class.</span></span> <span data-ttu-id="ca627-158">Výchozí konfigurace je:</span><span class="sxs-lookup"><span data-stu-id="ca627-158">The default configuration is:</span></span>

```csharp
builder.Entity<TUser>(b =>
{
    // Primary key
    b.HasKey(u => u.Id);

    // Indexes for "normalized" username and email, to allow efficient lookups
    b.HasIndex(u => u.NormalizedUserName).HasName("UserNameIndex").IsUnique();
    b.HasIndex(u => u.NormalizedEmail).HasName("EmailIndex");

    // Maps to the AspNetUsers table
    b.ToTable("AspNetUsers");

    // A concurrency token for use with the optimistic concurrency checking
    b.Property(u => u.ConcurrencyStamp).IsConcurrencyToken();

    // Limit the size of columns to use efficient database types
    b.Property(u => u.UserName).HasMaxLength(256);
    b.Property(u => u.NormalizedUserName).HasMaxLength(256);
    b.Property(u => u.Email).HasMaxLength(256);
    b.Property(u => u.NormalizedEmail).HasMaxLength(256);

    // The relationships between User and other entity types
    // Note that these relationships are configured with no navigation properties

    // Each User can have many UserClaims
    b.HasMany<TUserClaim>().WithOne().HasForeignKey(uc => uc.UserId).IsRequired();

    // Each User can have many UserLogins
    b.HasMany<TUserLogin>().WithOne().HasForeignKey(ul => ul.UserId).IsRequired();

    // Each User can have many UserTokens
    b.HasMany<TUserToken>().WithOne().HasForeignKey(ut => ut.UserId).IsRequired();

    // Each User can have many entries in the UserRole join table
    b.HasMany<TUserRole>().WithOne().HasForeignKey(ur => ur.UserId).IsRequired();
});

builder.Entity<TUserClaim>(b =>
{
    // Primary key
    b.HasKey(uc => uc.Id);

    // Maps to the AspNetUserClaims table
    b.ToTable("AspNetUserClaims");
});

builder.Entity<TUserLogin>(b =>
{
    // Composite primary key consisting of the LoginProvider and the key to use
    // with that provider
    b.HasKey(l => new { l.LoginProvider, l.ProviderKey });

    // Limit the size of the composite key columns due to common DB restrictions
    b.Property(l => l.LoginProvider).HasMaxLength(128);
    b.Property(l => l.ProviderKey).HasMaxLength(128);

    // Maps to the AspNetUserLogins table
    b.ToTable("AspNetUserLogins");
});

builder.Entity<TUserToken>(b =>
{
    // Composite primary key consisting of the UserId, LoginProvider and Name
    b.HasKey(t => new { t.UserId, t.LoginProvider, t.Name });

    // Limit the size of the composite key columns due to common DB restrictions
    b.Property(t => t.LoginProvider).HasMaxLength(maxKeyLength);
    b.Property(t => t.Name).HasMaxLength(maxKeyLength);

    // Maps to the AspNetUserTokens table
    b.ToTable("AspNetUserTokens");
});

builder.Entity<TRole>(b =>
{
    // Primary key
    b.HasKey(r => r.Id);

    // Index for "normalized" role name to allow efficient lookups
    b.HasIndex(r => r.NormalizedName).HasName("RoleNameIndex").IsUnique();

    // Maps to the AspNetRoles table
    b.ToTable("AspNetRoles");

    // A concurrency token for use with the optimistic concurrency checking
    b.Property(r => r.ConcurrencyStamp).IsConcurrencyToken();

    // Limit the size of columns to use efficient database types
    b.Property(u => u.Name).HasMaxLength(256);
    b.Property(u => u.NormalizedName).HasMaxLength(256);

    // The relationships between Role and other entity types
    // Note that these relationships are configured with no navigation properties

    // Each Role can have many entries in the UserRole join table
    b.HasMany<TUserRole>().WithOne().HasForeignKey(ur => ur.RoleId).IsRequired();

    // Each Role can have many associated RoleClaims
    b.HasMany<TRoleClaim>().WithOne().HasForeignKey(rc => rc.RoleId).IsRequired();
});

builder.Entity<TRoleClaim>(b =>
{
    // Primary key
    b.HasKey(rc => rc.Id);

    // Maps to the AspNetRoleClaims table
    b.ToTable("AspNetRoleClaims");
});

builder.Entity<TUserRole>(b =>
{
    // Primary key
    b.HasKey(r => new { r.UserId, r.RoleId });

    // Maps to the AspNetUserRoles table
    b.ToTable("AspNetUserRoles");
});
```

### <a name="model-generic-types"></a><span data-ttu-id="ca627-159">Obecné typy modelu</span><span class="sxs-lookup"><span data-stu-id="ca627-159">Model generic types</span></span>

<span data-ttu-id="ca627-160">Identity definuje výchozí [Common Language Runtime](/dotnet/standard/glossary#clr) výše uvedených typů (CLR) pro každý typ entity.</span><span class="sxs-lookup"><span data-stu-id="ca627-160">Identity defines default [Common Language Runtime](/dotnet/standard/glossary#clr) (CLR) types for each of the entity types listed above.</span></span> <span data-ttu-id="ca627-161">Tyto typy jsou předponu *Identity*:</span><span class="sxs-lookup"><span data-stu-id="ca627-161">These types are all prefixed with *Identity*:</span></span>

* `IdentityUser`
* `IdentityRole`
* `IdentityUserClaim`
* `IdentityUserToken`
* `IdentityUserLogin`
* `IdentityRoleClaim`
* `IdentityUserRole`

<span data-ttu-id="ca627-162">Místo použití těchto typů přímo, typy slouží jako základní třídy pro aplikace pro vlastní typy.</span><span class="sxs-lookup"><span data-stu-id="ca627-162">Rather than using these types directly, the types can be used as base classes for the app's own types.</span></span> <span data-ttu-id="ca627-163">`DbContext` Tříd definovaných výčtem Identity jsou obecné, tak, že různé typy CLR lze použít pro jeden nebo více typů entit v modelu.</span><span class="sxs-lookup"><span data-stu-id="ca627-163">The `DbContext` classes defined by Identity are generic, such that different CLR types can be used for one or more of the entity types in the model.</span></span> <span data-ttu-id="ca627-164">Také umožní tyto obecné typy `User` primární klíč (PK) datový typ změnit.</span><span class="sxs-lookup"><span data-stu-id="ca627-164">These generic types also allow the `User` primary key (PK) data type to be changed.</span></span>

<span data-ttu-id="ca627-165">Při použití identit s podporou pro role, <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext> třída by měla být použita.</span><span class="sxs-lookup"><span data-stu-id="ca627-165">When using Identity with support for roles, an <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext> class should be used.</span></span> <span data-ttu-id="ca627-166">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ca627-166">For example:</span></span>

```csharp
// Uses all the built-in Identity types
// Uses `string` as the key type
public class IdentityDbContext
    : IdentityDbContext<IdentityUser, IdentityRole, string>
{
}

// Uses the built-in Identity types except with a custom User type
// Uses `string` as the key type
public class IdentityDbContext<TUser>
    : IdentityDbContext<TUser, IdentityRole, string>
        where TUser : IdentityUser
{
}

// Uses the built-in Identity types except with custom User and Role types
// The key type is defined by TKey
public class IdentityDbContext<TUser, TRole, TKey> : IdentityDbContext<
    TUser, TRole, TKey, IdentityUserClaim<TKey>, IdentityUserRole<TKey>,
    IdentityUserLogin<TKey>, IdentityRoleClaim<TKey>, IdentityUserToken<TKey>>
        where TUser : IdentityUser<TKey>
        where TRole : IdentityRole<TKey>
        where TKey : IEquatable<TKey>
{
}

// No built-in Identity types are used; all are specified by generic arguments
// The key type is defined by TKey
public abstract class IdentityDbContext<
    TUser, TRole, TKey, TUserClaim, TUserRole, TUserLogin, TRoleClaim, TUserToken>
    : IdentityUserContext<TUser, TKey, TUserClaim, TUserLogin, TUserToken>
         where TUser : IdentityUser<TKey>
         where TRole : IdentityRole<TKey>
         where TKey : IEquatable<TKey>
         where TUserClaim : IdentityUserClaim<TKey>
         where TUserRole : IdentityUserRole<TKey>
         where TUserLogin : IdentityUserLogin<TKey>
         where TRoleClaim : IdentityRoleClaim<TKey>
         where TUserToken : IdentityUserToken<TKey>
```

<span data-ttu-id="ca627-167">Je také možné použít Identity bez role (jenom deklarace identity), v takovém případě <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUserContext`1> třída by měla být použita:</span><span class="sxs-lookup"><span data-stu-id="ca627-167">It's also possible to use Identity without roles (only claims), in which case an <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUserContext`1> class should be used:</span></span>

```csharp
// Uses the built-in non-role Identity types except with a custom User type
// Uses `string` as the key type
public class IdentityUserContext<TUser>
    : IdentityUserContext<TUser, string>
        where TUser : IdentityUser
{
}

// Uses the built-in non-role Identity types except with a custom User type
// The key type is defined by TKey
public class IdentityUserContext<TUser, TKey> : IdentityUserContext<
    TUser, TKey, IdentityUserClaim<TKey>, IdentityUserLogin<TKey>,
    IdentityUserToken<TKey>>
        where TUser : IdentityUser<TKey>
        where TKey : IEquatable<TKey>
{
}

// No built-in Identity types are used; all are specified by generic arguments, with no roles
// The key type is defined by TKey
public abstract class IdentityUserContext<
    TUser, TKey, TUserClaim, TUserLogin, TUserToken> : DbContext
        where TUser : IdentityUser<TKey>
        where TKey : IEquatable<TKey>
        where TUserClaim : IdentityUserClaim<TKey>
        where TUserLogin : IdentityUserLogin<TKey>
        where TUserToken : IdentityUserToken<TKey>
{
}
```

## <a name="customize-the-model"></a><span data-ttu-id="ca627-168">Přizpůsobení modelu</span><span class="sxs-lookup"><span data-stu-id="ca627-168">Customize the model</span></span>

<span data-ttu-id="ca627-169">Výchozí bod pro přizpůsobení modelu je odvozen od typu odpovídající kontext.</span><span class="sxs-lookup"><span data-stu-id="ca627-169">The starting point for model customization is to derive from the appropriate context type.</span></span> <span data-ttu-id="ca627-170">Najdete v článku [Model obecných typů](#model-generic-types) oddílu.</span><span class="sxs-lookup"><span data-stu-id="ca627-170">See the [Model generic types](#model-generic-types) section.</span></span> <span data-ttu-id="ca627-171">Tento typ kontextu se běžně označuje `ApplicationDbContext` a je vytvořen pomocí šablony ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="ca627-171">This context type is customarily called `ApplicationDbContext` and is created by the ASP.NET Core templates.</span></span>

<span data-ttu-id="ca627-172">Kontext se používá ke konfiguraci modelu dvěma způsoby:</span><span class="sxs-lookup"><span data-stu-id="ca627-172">The context is used to configure the model in two ways:</span></span>

* <span data-ttu-id="ca627-173">Zadání entity a typy klíčů pro parametry obecného typu.</span><span class="sxs-lookup"><span data-stu-id="ca627-173">Supplying entity and key types for the generic type parameters.</span></span>
* <span data-ttu-id="ca627-174">Přepsání `OnModelCreating` upravit mapování z těchto typů.</span><span class="sxs-lookup"><span data-stu-id="ca627-174">Overriding `OnModelCreating` to modify the mapping of these types.</span></span>

<span data-ttu-id="ca627-175">Při přepisování `OnModelCreating`, `base.OnModelCreating` by měla být volána nejprve; dále by měla být volána přepsání konfigurace.</span><span class="sxs-lookup"><span data-stu-id="ca627-175">When overriding `OnModelCreating`, `base.OnModelCreating` should be called first; the overriding configuration should be called next.</span></span> <span data-ttu-id="ca627-176">EF Core má obvykle služby wins poslední jednu zásadu konfigurace.</span><span class="sxs-lookup"><span data-stu-id="ca627-176">EF Core generally has a last-one-wins policy for configuration.</span></span> <span data-ttu-id="ca627-177">Například pokud `ToTable` nejdříve volána metoda pro určitý typ entity s názvem jedné tabulky a pak znovu později s názvem jinou tabulku, název tabulky do druhé volání se používá.</span><span class="sxs-lookup"><span data-stu-id="ca627-177">For example, if the `ToTable` method for an entity type is called first with one table name and then again later with a different table name, the table name in the second call is used.</span></span>

### <a name="custom-user-data"></a><span data-ttu-id="ca627-178">Vlastní uživatelská data</span><span class="sxs-lookup"><span data-stu-id="ca627-178">Custom user data</span></span>

<span data-ttu-id="ca627-179">[Vlastní uživatelská data](xref:security/authentication/add-user-data) podporuje dědění z `IdentityUser`.</span><span class="sxs-lookup"><span data-stu-id="ca627-179">[Custom user data](xref:security/authentication/add-user-data) is supported by inheriting from `IdentityUser`.</span></span> <span data-ttu-id="ca627-180">Je to obvyklé název tohoto typu `ApplicationUser`:</span><span class="sxs-lookup"><span data-stu-id="ca627-180">It's customary to name this type `ApplicationUser`:</span></span>


```csharp
public class ApplicationUser : IdentityUser
{
    public string CustomTag { get; set; }
}
```

<span data-ttu-id="ca627-181">Použití `ApplicationUser` typem jako argumentem obecného kontextu:</span><span class="sxs-lookup"><span data-stu-id="ca627-181">Use the `ApplicationUser` type as a generic argument for the context:</span></span>

```csharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

<span data-ttu-id="ca627-182">Není nutné přepsat `OnModelCreating` v `ApplicationDbContext` třídy.</span><span class="sxs-lookup"><span data-stu-id="ca627-182">There's no need to override `OnModelCreating` in the `ApplicationDbContext` class.</span></span> <span data-ttu-id="ca627-183">EF Core mapuje `CustomTag` vlastnost konvencí.</span><span class="sxs-lookup"><span data-stu-id="ca627-183">EF Core maps the `CustomTag` property by convention.</span></span> <span data-ttu-id="ca627-184">Ale potřeba aktualizovat k vytvoření nové databáze `CustomTag` sloupce.</span><span class="sxs-lookup"><span data-stu-id="ca627-184">However, the database needs to be updated to create a new `CustomTag` column.</span></span> <span data-ttu-id="ca627-185">Chcete-li vytvořit sloupec, přidejte migraci a pak aktualizujte databázi, jak je popsáno v [Identity a migrace EF Core](#identity-and-ef-core-migrations).</span><span class="sxs-lookup"><span data-stu-id="ca627-185">To create the column, add a migration, and then update the database as described in [Identity and EF Core Migrations](#identity-and-ef-core-migrations).</span></span>

<span data-ttu-id="ca627-186">Aktualizace `Startup.ConfigureServices` použití nového `ApplicationUser` třídy:</span><span class="sxs-lookup"><span data-stu-id="ca627-186">Update `Startup.ConfigureServices` to use the new `ApplicationUser` class:</span></span>

::: moniker range=">= aspnetcore-2.1"

```csharp
services.AddDefaultIdentity<ApplicationUser>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultUI();
```

<span data-ttu-id="ca627-187">V ASP.NET Core 2.1 nebo novější je identita ve formě knihovny tříd Razor.</span><span class="sxs-lookup"><span data-stu-id="ca627-187">In ASP.NET Core 2.1 or later, Identity is provided as a Razor Class Library.</span></span> <span data-ttu-id="ca627-188">Další informace naleznete v tématu <xref:security/authentication/scaffold-identity>.</span><span class="sxs-lookup"><span data-stu-id="ca627-188">For more information, see <xref:security/authentication/scaffold-identity>.</span></span> <span data-ttu-id="ca627-189">V důsledku toho předcházející kód vyžaduje volání <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span><span class="sxs-lookup"><span data-stu-id="ca627-189">Consequently, the preceding code requires a call to <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span></span> <span data-ttu-id="ca627-190">Pokud generátor Identity se použil k přidání Identity soubory do projektu, odeberte volání `AddDefaultUI`.</span><span class="sxs-lookup"><span data-stu-id="ca627-190">If the Identity scaffolder was used to add Identity files to the project, remove the call to `AddDefaultUI`.</span></span> <span data-ttu-id="ca627-191">Další informace naleznete v tématu:</span><span class="sxs-lookup"><span data-stu-id="ca627-191">For more information, see:</span></span>

* [<span data-ttu-id="ca627-192">Vygenerování identity</span><span class="sxs-lookup"><span data-stu-id="ca627-192">Scaffold Identity</span></span>](xref:security/authentication/scaffold-identity)
* [<span data-ttu-id="ca627-193">Přidat, stáhněte si a odstranit vlastní uživatelská data na identitu</span><span class="sxs-lookup"><span data-stu-id="ca627-193">Add, download, and delete custom user data to Identity</span></span>](xref:security/authentication/add-user-data)

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();
```

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext, Guid>()
        .AddDefaultTokenProviders();
```

::: moniker-end

### <a name="change-the-primary-key-type"></a><span data-ttu-id="ca627-194">Změnit typ primárního klíče</span><span class="sxs-lookup"><span data-stu-id="ca627-194">Change the primary key type</span></span>

<span data-ttu-id="ca627-195">Změnit na datový typ sloupce PK po vytvoření databáze je problematické u řada databázových systémů.</span><span class="sxs-lookup"><span data-stu-id="ca627-195">A change to the PK column's data type after the database has been created is problematic on many database systems.</span></span> <span data-ttu-id="ca627-196">Změna primárnímu Klíči obvykle zahrnuje vyřadit a znovu vytvořit v tabulce.</span><span class="sxs-lookup"><span data-stu-id="ca627-196">Changing the PK typically involves dropping and re-creating the table.</span></span> <span data-ttu-id="ca627-197">Proto typy klíčů musí být zadán v počáteční migraci při vytvoření databáze.</span><span class="sxs-lookup"><span data-stu-id="ca627-197">Therefore, key types should be specified in the initial migration when the database is created.</span></span>

<span data-ttu-id="ca627-198">Použijte následující postup změna typu PK:</span><span class="sxs-lookup"><span data-stu-id="ca627-198">Follow these steps to change the PK type:</span></span>

1. <span data-ttu-id="ca627-199">Pokud byla vytvořena databáze před změnou PK spustit `Drop-Database` (PMC) nebo `dotnet ef database drop` (.NET Core CLI) k jeho odstranění.</span><span class="sxs-lookup"><span data-stu-id="ca627-199">If the database was created before the PK change, run `Drop-Database` (PMC) or `dotnet ef database drop` (.NET Core CLI) to delete it.</span></span>
2. <span data-ttu-id="ca627-200">Po potvrzení databáze, odebrat úvodní migrace s `Remove-Migration` (PMC) nebo `dotnet ef migrations remove` (.NET Core CLI).</span><span class="sxs-lookup"><span data-stu-id="ca627-200">After confirming deletion of the database, remove the initial migration with `Remove-Migration` (PMC) or `dotnet ef migrations remove` (.NET Core CLI).</span></span>
3. <span data-ttu-id="ca627-201">Aktualizace `ApplicationDbContext` třídy odvozovat z <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext`3>.</span><span class="sxs-lookup"><span data-stu-id="ca627-201">Update the `ApplicationDbContext` class to derive from <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext`3>.</span></span> <span data-ttu-id="ca627-202">Zadejte nový typ klíče pro `TKey`.</span><span class="sxs-lookup"><span data-stu-id="ca627-202">Specify the new key type for `TKey`.</span></span> <span data-ttu-id="ca627-203">Například pro použití `Guid` typ klíče:</span><span class="sxs-lookup"><span data-stu-id="ca627-203">For example, to use a `Guid` key type:</span></span>

    ```csharp
    public class ApplicationDbContext
        : IdentityDbContext<IdentityUser<Guid>, IdentityRole<Guid>, Guid>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }
    }
    ```

    ::: moniker range=">= aspnetcore-2.0"

    <span data-ttu-id="ca627-204">V předchozím kódu, obecné třídy <xref:Microsoft.AspNetCore.Identity.IdentityUser`1> a <xref:Microsoft.AspNetCore.Identity.IdentityRole`1> použít nový typ klíče musí být zadán.</span><span class="sxs-lookup"><span data-stu-id="ca627-204">In the preceding code, the generic classes <xref:Microsoft.AspNetCore.Identity.IdentityUser`1> and <xref:Microsoft.AspNetCore.Identity.IdentityRole`1> must be specified to use the new key type.</span></span>

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    <span data-ttu-id="ca627-205">V předchozím kódu, obecné třídy <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUser`1> a <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityRole`1> použít nový typ klíče musí být zadán.</span><span class="sxs-lookup"><span data-stu-id="ca627-205">In the preceding code, the generic classes <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUser`1> and <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityRole`1> must be specified to use the new key type.</span></span>

    ::: moniker-end

    <span data-ttu-id="ca627-206">`Startup.ConfigureServices` musí být aktualizován na použití obecných uživatele:</span><span class="sxs-lookup"><span data-stu-id="ca627-206">`Startup.ConfigureServices` must be updated to use the generic user:</span></span>

    ::: moniker range=">= aspnetcore-2.1"

    ```csharp
    services.AddDefaultIdentity<IdentityUser<Guid>>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();
    ```

    ::: moniker-end

    ::: moniker range="= aspnetcore-2.0"

    ```csharp
    services.AddIdentity<IdentityUser<Guid>, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();
    ```

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    ```csharp
    services.AddIdentity<IdentityUser<Guid>, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext, Guid>()
            .AddDefaultTokenProviders();
    ```

    ::: moniker-end

4. <span data-ttu-id="ca627-207">Pokud vlastní `ApplicationUser` používá třídy, aktualizaci třídy, která se dědí z `IdentityUser`.</span><span class="sxs-lookup"><span data-stu-id="ca627-207">If a custom `ApplicationUser` class is being used, update the class to inherit from `IdentityUser`.</span></span> <span data-ttu-id="ca627-208">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ca627-208">For example:</span></span>

    ::: moniker range="<= aspnetcore-1.1"

    [!code-csharp[](customize-identity-model/samples/1.1/MvcSampleApp/Models/ApplicationUser.cs?name=snippet_ApplicationUser&highlight=4)]

    ::: moniker-end

    ::: moniker range=">= aspnetcore-2.0"

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Data/ApplicationUser.cs?name=snippet_ApplicationUser&highlight=4)]

    ::: moniker-end

    <span data-ttu-id="ca627-209">Aktualizace `ApplicationDbContext` tak, aby odkazovaly vlastní `ApplicationUser` třídy:</span><span class="sxs-lookup"><span data-stu-id="ca627-209">Update `ApplicationDbContext` to reference the custom `ApplicationUser` class:</span></span>

    ```csharp
    public class ApplicationDbContext
        : IdentityDbContext<ApplicationUser, IdentityRole<Guid>, Guid>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }
    }
    ```

    <span data-ttu-id="ca627-210">Registrovat třídu kontext vlastní databázi, při přidávání služba identit v `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="ca627-210">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    ::: moniker range=">= aspnetcore-2.1"

    ```csharp
    services.AddDefaultIdentity<ApplicationUser>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultUI()
            .AddDefaultTokenProviders();
    ```

    <span data-ttu-id="ca627-211">Primární klíč datový typ je odvozen díky analýze <xref:Microsoft.EntityFrameworkCore.DbContext> objektu.</span><span class="sxs-lookup"><span data-stu-id="ca627-211">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    <span data-ttu-id="ca627-212">V ASP.NET Core 2.1 nebo novější je identita ve formě knihovny tříd Razor.</span><span class="sxs-lookup"><span data-stu-id="ca627-212">In ASP.NET Core 2.1 or later, Identity is provided as a Razor Class Library.</span></span> <span data-ttu-id="ca627-213">Další informace naleznete v tématu <xref:security/authentication/scaffold-identity>.</span><span class="sxs-lookup"><span data-stu-id="ca627-213">For more information, see <xref:security/authentication/scaffold-identity>.</span></span> <span data-ttu-id="ca627-214">V důsledku toho předcházející kód vyžaduje volání <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span><span class="sxs-lookup"><span data-stu-id="ca627-214">Consequently, the preceding code requires a call to <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span></span> <span data-ttu-id="ca627-215">Pokud generátor Identity se použil k přidání Identity soubory do projektu, odeberte volání `AddDefaultUI`.</span><span class="sxs-lookup"><span data-stu-id="ca627-215">If the Identity scaffolder was used to add Identity files to the project, remove the call to `AddDefaultUI`.</span></span>

    ::: moniker-end

    ::: moniker range="= aspnetcore-2.0"

    ```csharp
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();
    ```

    <span data-ttu-id="ca627-216">Primární klíč datový typ je odvozen díky analýze <xref:Microsoft.EntityFrameworkCore.DbContext> objektu.</span><span class="sxs-lookup"><span data-stu-id="ca627-216">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    ```csharp
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext, Guid>()
            .AddDefaultTokenProviders();
    ```

    <span data-ttu-id="ca627-217"><xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> Metoda přijímá `TKey` typ určující primární klíč datového typu.</span><span class="sxs-lookup"><span data-stu-id="ca627-217">The <xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> method accepts a `TKey` type indicating the primary key's data type.</span></span>

    ::: moniker-end

5. <span data-ttu-id="ca627-218">Pokud vlastní `ApplicationRole` používá třídy, aktualizaci třídy, která se dědí z `IdentityRole<TKey>`.</span><span class="sxs-lookup"><span data-stu-id="ca627-218">If a custom `ApplicationRole` class is being used, update the class to inherit from `IdentityRole<TKey>`.</span></span> <span data-ttu-id="ca627-219">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ca627-219">For example:</span></span>

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Data/ApplicationRole.cs?name=snippet_ApplicationRole&highlight=4)]

    <span data-ttu-id="ca627-220">Aktualizace `ApplicationDbContext` tak, aby odkazovaly vlastní `ApplicationRole` třídy.</span><span class="sxs-lookup"><span data-stu-id="ca627-220">Update `ApplicationDbContext` to reference the custom `ApplicationRole` class.</span></span> <span data-ttu-id="ca627-221">Například následující třídy odkazuje na vlastní `ApplicationUser` a vlastní `ApplicationRole`:</span><span class="sxs-lookup"><span data-stu-id="ca627-221">For example, the following class references a custom `ApplicationUser` and a custom `ApplicationRole`:</span></span>

    ::: moniker range=">= aspnetcore-2.1"

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Data/ApplicationDbContext.cs?name=snippet_ApplicationDbContext&highlight=5-6)]

    <span data-ttu-id="ca627-222">Registrovat třídu kontext vlastní databázi, při přidávání služba identit v `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="ca627-222">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Startup.cs?name=snippet_ConfigureServices&highlight=13-16)]

    <span data-ttu-id="ca627-223">Primární klíč datový typ je odvozen díky analýze <xref:Microsoft.EntityFrameworkCore.DbContext> objektu.</span><span class="sxs-lookup"><span data-stu-id="ca627-223">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    <span data-ttu-id="ca627-224">V ASP.NET Core 2.1 nebo novější je identita ve formě knihovny tříd Razor.</span><span class="sxs-lookup"><span data-stu-id="ca627-224">In ASP.NET Core 2.1 or later, Identity is provided as a Razor Class Library.</span></span> <span data-ttu-id="ca627-225">Další informace naleznete v tématu <xref:security/authentication/scaffold-identity>.</span><span class="sxs-lookup"><span data-stu-id="ca627-225">For more information, see <xref:security/authentication/scaffold-identity>.</span></span> <span data-ttu-id="ca627-226">V důsledku toho předcházející kód vyžaduje volání <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span><span class="sxs-lookup"><span data-stu-id="ca627-226">Consequently, the preceding code requires a call to <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span></span> <span data-ttu-id="ca627-227">Pokud generátor Identity se použil k přidání Identity soubory do projektu, odeberte volání `AddDefaultUI`.</span><span class="sxs-lookup"><span data-stu-id="ca627-227">If the Identity scaffolder was used to add Identity files to the project, remove the call to `AddDefaultUI`.</span></span>

    ::: moniker-end

    ::: moniker range="= aspnetcore-2.0"

    [!code-csharp[](customize-identity-model/samples/2.0/RazorPagesSampleApp/Data/ApplicationDbContext.cs?name=snippet_ApplicationDbContext&highlight=5-6)]

    <span data-ttu-id="ca627-228">Registrovat třídu kontext vlastní databázi, při přidávání služba identit v `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="ca627-228">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    [!code-csharp[](customize-identity-model/samples/2.0/RazorPagesSampleApp/Startup.cs?name=snippet_ConfigureServices&highlight=7-9)]

    <span data-ttu-id="ca627-229">Primární klíč datový typ je odvozen díky analýze <xref:Microsoft.EntityFrameworkCore.DbContext> objektu.</span><span class="sxs-lookup"><span data-stu-id="ca627-229">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    [!code-csharp[](customize-identity-model/samples/1.1/MvcSampleApp/Data/ApplicationDbContext.cs?name=snippet_ApplicationDbContext&highlight=5-6)]

    <span data-ttu-id="ca627-230">Registrovat třídu kontext vlastní databázi, při přidávání služba identit v `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="ca627-230">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    [!code-csharp[](customize-identity-model/samples/1.1/MvcSampleApp/Startup.cs?name=snippet_ConfigureServices&highlight=7-9)]

    <span data-ttu-id="ca627-231"><xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> Metoda přijímá `TKey` typ určující primární klíč datového typu.</span><span class="sxs-lookup"><span data-stu-id="ca627-231">The <xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> method accepts a `TKey` type indicating the primary key's data type.</span></span>

    ::: moniker-end

### <a name="add-navigation-properties"></a><span data-ttu-id="ca627-232">Přidání navigační vlastnosti</span><span class="sxs-lookup"><span data-stu-id="ca627-232">Add navigation properties</span></span>

<span data-ttu-id="ca627-233">Změna konfigurace modelu pro relace může být obtížnější než dělat jiné změny.</span><span class="sxs-lookup"><span data-stu-id="ca627-233">Changing the model configuration for relationships can be more difficult than making other changes.</span></span> <span data-ttu-id="ca627-234">Nahraďte existující relace, spíše než nový, vytvořit další relace musí věnovat pozornost.</span><span class="sxs-lookup"><span data-stu-id="ca627-234">Care must be taken to replace the existing relationships rather than create new, additional relationships.</span></span> <span data-ttu-id="ca627-235">Zejména změněné relaci je třeba určit stejné vlastnost cizího klíče (Cizíklíč) jako existující relaci.</span><span class="sxs-lookup"><span data-stu-id="ca627-235">In particular, the changed relationship must specify the same foreign key (FK) property as the existing relationship.</span></span> <span data-ttu-id="ca627-236">Například vztah mezi `Users` a `UserClaims` je ve výchozím nastavení zadané následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="ca627-236">For example, the relationship between `Users` and `UserClaims` is, by default, specified as follows:</span></span>

```csharp
builder.Entity<TUser>(b =>
{
    // Each User can have many UserClaims
    b.HasMany<TUserClaim>()
     .WithOne()
     .HasForeignKey(uc => uc.UserId)
     .IsRequired();
});
```

<span data-ttu-id="ca627-237">Cizího klíče pro tento vztah je stanoveno, `UserClaim.UserId` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="ca627-237">The FK for this relationship is specified as the `UserClaim.UserId` property.</span></span> <span data-ttu-id="ca627-238">`HasMany` a `WithOne` jsou volat bez argumentů a vytvořit tak relaci bez vlastnosti navigace.</span><span class="sxs-lookup"><span data-stu-id="ca627-238">`HasMany` and `WithOne` are called without arguments to create the relationship without navigation properties.</span></span>

<span data-ttu-id="ca627-239">Přidání navigační vlastnost pro `ApplicationUser` , která umožňuje přidružené `UserClaims` odkazovat od uživatele:</span><span class="sxs-lookup"><span data-stu-id="ca627-239">Add a navigation property to `ApplicationUser` that allows associated `UserClaims` to be referenced from the user:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
}
```

<span data-ttu-id="ca627-240">`TKey` Pro `IdentityUserClaim<TKey>` je typ zadaný pro PK uživatelů.</span><span class="sxs-lookup"><span data-stu-id="ca627-240">The `TKey` for `IdentityUserClaim<TKey>` is the type specified for the PK of users.</span></span> <span data-ttu-id="ca627-241">V takovém případě `TKey` je `string` vzhledem k tomu, že se používají výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="ca627-241">In this case, `TKey` is `string` because the defaults are being used.</span></span> <span data-ttu-id="ca627-242">Má **není** PK typ `UserClaim` typu entity.</span><span class="sxs-lookup"><span data-stu-id="ca627-242">It's **not** the PK type for the `UserClaim` entity type.</span></span>

<span data-ttu-id="ca627-243">Teď, když existuje navigační vlastnost, musí se nakonfigurovat v `OnModelCreating`:</span><span class="sxs-lookup"><span data-stu-id="ca627-243">Now that the navigation property exists, it must be configured in `OnModelCreating`:</span></span>

```csharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();
        });
    }
}
```

<span data-ttu-id="ca627-244">Všimněte si, že je přesně stejné jako dříve, jenom s navigační vlastnost zadanou ve volání do nakonfigurovaný vztah `HasMany`.</span><span class="sxs-lookup"><span data-stu-id="ca627-244">Notice that relationship is configured exactly as it was before, only with a navigation property specified in the call to `HasMany`.</span></span>

<span data-ttu-id="ca627-245">Vlastnosti navigace existují pouze v modelu EF, ne databáze.</span><span class="sxs-lookup"><span data-stu-id="ca627-245">The navigation properties only exist in the EF model, not the database.</span></span> <span data-ttu-id="ca627-246">Vzhledem k tomu, že nedošlo ke změně cizího klíče pro relaci, nevyžaduje, aby databáze, kterou chcete aktualizovat tento druh změny modelu.</span><span class="sxs-lookup"><span data-stu-id="ca627-246">Because the FK for the relationship hasn't changed, this kind of model change doesn't require the database to be updated.</span></span> <span data-ttu-id="ca627-247">To lze ověřit tak, že přidáte migrace po provedení změny.</span><span class="sxs-lookup"><span data-stu-id="ca627-247">This can be checked by adding a migration after making the change.</span></span> <span data-ttu-id="ca627-248">`Up` a `Down` metody jsou prázdné.</span><span class="sxs-lookup"><span data-stu-id="ca627-248">The `Up` and `Down` methods are empty.</span></span>

### <a name="add-all-user-navigation-properties"></a><span data-ttu-id="ca627-249">Přidat všechny uživatele navigační vlastnosti</span><span class="sxs-lookup"><span data-stu-id="ca627-249">Add all User navigation properties</span></span>

<span data-ttu-id="ca627-250">Pomocí výše uvedené části jako vodítko, v následujícím příkladu nakonfigurujeme jednosměrnou navigační vlastnosti pro všechny relace pro uživatele:</span><span class="sxs-lookup"><span data-stu-id="ca627-250">Using the section above as guidance, the following example configures unidirectional navigation properties for all relationships on User:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
    public virtual ICollection<IdentityUserLogin<string>> Logins { get; set; }
    public virtual ICollection<IdentityUserToken<string>> Tokens { get; set; }
    public virtual ICollection<IdentityUserRole<string>> UserRoles { get; set; }
}
```

```csharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne()
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne()
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne()
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });
    }
}
```

### <a name="add-user-and-role-navigation-properties"></a><span data-ttu-id="ca627-251">Přidat uživatele a roli navigační vlastnosti</span><span class="sxs-lookup"><span data-stu-id="ca627-251">Add User and Role navigation properties</span></span>

<span data-ttu-id="ca627-252">Pomocí výše uvedené části jako vodítko, v následujícím příkladu nakonfigurujeme navigačních vlastností u všech relací na uživatele a roli:</span><span class="sxs-lookup"><span data-stu-id="ca627-252">Using the section above as guidance, the following example configures navigation properties for all relationships on User and Role:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
    public virtual ICollection<IdentityUserLogin<string>> Logins { get; set; }
    public virtual ICollection<IdentityUserToken<string>> Tokens { get; set; }
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationRole : IdentityRole
{
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationUserRole : IdentityUserRole<string>
{
    public virtual ApplicationUser User { get; set; }
    public virtual ApplicationRole Role { get; set; }
}
```

```csharp
public class ApplicationDbContext
    : IdentityDbContext<
        ApplicationUser, ApplicationRole, string,
        IdentityUserClaim<string>, ApplicationUserRole, IdentityUserLogin<string>,
        IdentityRoleClaim<string>, IdentityUserToken<string>>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne()
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne()
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.User)
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });

        modelBuilder.Entity<ApplicationRole>(b =>
        {
            // Each Role can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.Role)
                .HasForeignKey(ur => ur.RoleId)
                .IsRequired();
        });

    }
}
```

<span data-ttu-id="ca627-253">Poznámky:</span><span class="sxs-lookup"><span data-stu-id="ca627-253">Notes:</span></span>

* <span data-ttu-id="ca627-254">Tento příklad zahrnuje také `UserRole` připojte se k entitě, která je nutná pro navigaci vztah many-to-many od uživatelů k rolím.</span><span class="sxs-lookup"><span data-stu-id="ca627-254">This example also includes the `UserRole` join entity, which is needed to navigate the many-to-many relationship from Users to Roles.</span></span>
* <span data-ttu-id="ca627-255">Nezapomeňte změnit typy navigačních vlastností, aby to odrážel `ApplicationXxx` typy jsou nyní používá místo `IdentityXxx` typy.</span><span class="sxs-lookup"><span data-stu-id="ca627-255">Remember to change the types of the navigation properties to reflect that `ApplicationXxx` types are now being used instead of `IdentityXxx` types.</span></span>
* <span data-ttu-id="ca627-256">Nezapomeňte použít `ApplicationXxx` v Obecné `ApplicationContext` definice.</span><span class="sxs-lookup"><span data-stu-id="ca627-256">Remember to use the `ApplicationXxx` in the generic `ApplicationContext` definition.</span></span>

### <a name="add-all-navigation-properties"></a><span data-ttu-id="ca627-257">Přidat všechny vlastnosti navigace</span><span class="sxs-lookup"><span data-stu-id="ca627-257">Add all navigation properties</span></span>

<span data-ttu-id="ca627-258">Pomocí výše uvedené části jako vodítko, v následujícím příkladu nakonfigurujeme navigační vlastnosti pro všechny relace na všechny typy entit:</span><span class="sxs-lookup"><span data-stu-id="ca627-258">Using the section above as guidance, the following example configures navigation properties for all relationships on all entity types:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<ApplicationUserClaim> Claims { get; set; }
    public virtual ICollection<ApplicationUserLogin> Logins { get; set; }
    public virtual ICollection<ApplicationUserToken> Tokens { get; set; }
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationRole : IdentityRole
{
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
    public virtual ICollection<ApplicationRoleClaim> RoleClaims { get; set; }
}

public class ApplicationUserRole : IdentityUserRole<string>
{
    public virtual ApplicationUser User { get; set; }
    public virtual ApplicationRole Role { get; set; }
}

public class ApplicationUserClaim : IdentityUserClaim<string>
{
    public virtual ApplicationUser User { get; set; }
}

public class ApplicationUserLogin : IdentityUserLogin<string>
{
    public virtual ApplicationUser User { get; set; }
}

public class ApplicationRoleClaim : IdentityRoleClaim<string>
{
    public virtual ApplicationRole Role { get; set; }
}

public class ApplicationUserToken : IdentityUserToken<string>
{
    public virtual ApplicationUser User { get; set; }
}
```

```csharp
public class ApplicationDbContext
    : IdentityDbContext<
        ApplicationUser, ApplicationRole, string,
        ApplicationUserClaim, ApplicationUserRole, ApplicationUserLogin,
        ApplicationRoleClaim, ApplicationUserToken>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne(e => e.User)
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne(e => e.User)
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne(e => e.User)
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.User)
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });

        modelBuilder.Entity<ApplicationRole>(b =>
        {
            // Each Role can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.Role)
                .HasForeignKey(ur => ur.RoleId)
                .IsRequired();

            // Each Role can have many associated RoleClaims
            b.HasMany(e => e.RoleClaims)
                .WithOne(e => e.Role)
                .HasForeignKey(rc => rc.RoleId)
                .IsRequired();
        });
    }
}
```

### <a name="use-composite-keys"></a><span data-ttu-id="ca627-259">Pomocí složených klíčů</span><span class="sxs-lookup"><span data-stu-id="ca627-259">Use composite keys</span></span>

<span data-ttu-id="ca627-260">V předchozích částech jsme vám ukázali, změna typu klíče, použít v modelu Identity.</span><span class="sxs-lookup"><span data-stu-id="ca627-260">The preceding sections demonstrated changing the type of key used in the Identity model.</span></span> <span data-ttu-id="ca627-261">Změna klíčů model Identity, který se má použít složené klíče není podporován nebo doporučené.</span><span class="sxs-lookup"><span data-stu-id="ca627-261">Changing the Identity key model to use composite keys isn't supported or recommended.</span></span> <span data-ttu-id="ca627-262">Složený klíč pomocí Identity postup zahrnuje změnu, jak kód Identity Manageru komunikuje s modelem.</span><span class="sxs-lookup"><span data-stu-id="ca627-262">Using a composite key with Identity involves changing how the Identity manager code interacts with the model.</span></span> <span data-ttu-id="ca627-263">Toto přizpůsobení je nad rámec tohoto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="ca627-263">This customization is beyond the scope of this document.</span></span>

### <a name="change-tablecolumn-names-and-facets"></a><span data-ttu-id="ca627-264">Změňte názvy tabulek nebo sloupců a omezující vlastnosti</span><span class="sxs-lookup"><span data-stu-id="ca627-264">Change table/column names and facets</span></span>

<span data-ttu-id="ca627-265">Chcete-li změnit názvy tabulek a sloupců, zavolejte `base.OnModelCreating`.</span><span class="sxs-lookup"><span data-stu-id="ca627-265">To change the names of tables and columns, call `base.OnModelCreating`.</span></span> <span data-ttu-id="ca627-266">Pak přidejte konfiguraci přepsat všechny výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="ca627-266">Then, add configuration to override any of the defaults.</span></span> <span data-ttu-id="ca627-267">Chcete-li například změnit název všech tabulek Identity:</span><span class="sxs-lookup"><span data-stu-id="ca627-267">For example, to change the name of all the Identity tables:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.ToTable("MyUsers");
    });

    modelBuilder.Entity<IdentityUserClaim<string>>(b =>
    {
        b.ToTable("MyUserClaims");
    });

    modelBuilder.Entity<IdentityUserLogin<string>>(b =>
    {
        b.ToTable("MyUserLogins");
    });

    modelBuilder.Entity<IdentityUserToken<string>>(b =>
    {
        b.ToTable("MyUserTokens");
    });

    modelBuilder.Entity<IdentityRole>(b =>
    {
        b.ToTable("MyRoles");
    });

    modelBuilder.Entity<IdentityRoleClaim<string>>(b =>
    {
        b.ToTable("MyRoleClaims");
    });

    modelBuilder.Entity<IdentityUserRole<string>>(b =>
    {
        b.ToTable("MyUserRoles");
    });
}
```

<span data-ttu-id="ca627-268">Tyto příklady používají výchozí typy Identity.</span><span class="sxs-lookup"><span data-stu-id="ca627-268">These examples use the default Identity types.</span></span> <span data-ttu-id="ca627-269">Pokud se používá jako typ aplikace. `ApplicationUser`, nakonfigurujte tento typ namísto výchozího typu.</span><span class="sxs-lookup"><span data-stu-id="ca627-269">If using an app type such as `ApplicationUser`, configure that type instead of the default type.</span></span>

<span data-ttu-id="ca627-270">Následující příklad změní některé názvy sloupců:</span><span class="sxs-lookup"><span data-stu-id="ca627-270">The following example changes some column names:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.Property(e => e.Email).HasColumnName("EMail");
    });

    modelBuilder.Entity<IdentityUserClaim<string>>(b =>
    {
        b.Property(e => e.ClaimType).HasColumnName("CType");
        b.Property(e => e.ClaimValue).HasColumnName("CValue");
    });
}
```

<span data-ttu-id="ca627-271">Některé typy sloupců databáze může mít nakonfigurovanou určité *omezující vlastnosti* (například maximální `string` povolená délka).</span><span class="sxs-lookup"><span data-stu-id="ca627-271">Some types of database columns can be configured with certain *facets* (for example, the maximum `string` length allowed).</span></span> <span data-ttu-id="ca627-272">Následující příklad nastaví maximální délka sloupce pro několik `string` vlastnosti v modelu:</span><span class="sxs-lookup"><span data-stu-id="ca627-272">The following example sets column maximum lengths for several `string` properties in the model:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.Property(u => u.UserName).HasMaxLength(128);
        b.Property(u => u.NormalizedUserName).HasMaxLength(128);
        b.Property(u => u.Email).HasMaxLength(128);
        b.Property(u => u.NormalizedEmail).HasMaxLength(128);
    });

    modelBuilder.Entity<IdentityUserToken<string>>(b =>
    {
        b.Property(t => t.LoginProvider).HasMaxLength(128);
        b.Property(t => t.Name).HasMaxLength(128);
    });
}
```

### <a name="map-to-a-different-schema"></a><span data-ttu-id="ca627-273">Mapování na jiné schéma</span><span class="sxs-lookup"><span data-stu-id="ca627-273">Map to a different schema</span></span>

<span data-ttu-id="ca627-274">Schémata může chovat jinak napříč poskytovatelé databází.</span><span class="sxs-lookup"><span data-stu-id="ca627-274">Schemas can behave differently across database providers.</span></span> <span data-ttu-id="ca627-275">Pro SQL Server, ve výchozím nastavení je vytvořit všechny tabulky v *dbo* schématu.</span><span class="sxs-lookup"><span data-stu-id="ca627-275">For SQL Server, the default is to create all tables in the *dbo* schema.</span></span> <span data-ttu-id="ca627-276">Tabulky lze vytvořit v jiné schéma.</span><span class="sxs-lookup"><span data-stu-id="ca627-276">The tables can be created in a different schema.</span></span> <span data-ttu-id="ca627-277">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ca627-277">For example:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.HasDefaultSchema("notdbo");
}
```

::: moniker range=">= aspnetcore-2.1"

### <a name="lazy-loading"></a><span data-ttu-id="ca627-278">Opožděné načtení</span><span class="sxs-lookup"><span data-stu-id="ca627-278">Lazy loading</span></span>

<span data-ttu-id="ca627-279">V této části se přidá podporu pro proxy opožděné načtení do modelu identit.</span><span class="sxs-lookup"><span data-stu-id="ca627-279">In this section, support for lazy-loading proxies in the Identity model is added.</span></span> <span data-ttu-id="ca627-280">Opožděné načtení je užitečné, protože umožňuje navigační vlastnosti bez první zajištění, která jste načetli.</span><span class="sxs-lookup"><span data-stu-id="ca627-280">Lazy-loading is useful since it allows navigation properties to be used without first ensuring they're loaded.</span></span>

<span data-ttu-id="ca627-281">Typy entit provádět vhodný pro opožděné načtení několika způsoby, jak je popsáno v [EF Core dokumentaci](/ef/core/querying/related-data#lazy-loading).</span><span class="sxs-lookup"><span data-stu-id="ca627-281">Entity types can be made suitable for lazy-loading in several ways, as described in the [EF Core documentation](/ef/core/querying/related-data#lazy-loading).</span></span> <span data-ttu-id="ca627-282">Pro jednoduchost použijte opožděné načtení proxy, což vyžaduje:</span><span class="sxs-lookup"><span data-stu-id="ca627-282">For simplicity, use lazy-loading proxies, which requires:</span></span>

* <span data-ttu-id="ca627-283">Instalace [Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/) balíčku.</span><span class="sxs-lookup"><span data-stu-id="ca627-283">Installation of the [Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/) package.</span></span>
* <span data-ttu-id="ca627-284">Volání <xref:Microsoft.EntityFrameworkCore.ProxiesExtensions.UseLazyLoadingProxies*> uvnitř <xref:Microsoft.Extensions.DependencyInjection.EntityFrameworkServiceCollectionExtensions.AddDbContext*>.</span><span class="sxs-lookup"><span data-stu-id="ca627-284">A call to <xref:Microsoft.EntityFrameworkCore.ProxiesExtensions.UseLazyLoadingProxies*> inside <xref:Microsoft.Extensions.DependencyInjection.EntityFrameworkServiceCollectionExtensions.AddDbContext*>.</span></span>
* <span data-ttu-id="ca627-285">Typy subjekt `public virtual` navigační vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="ca627-285">Public entity types with `public virtual` navigation properties.</span></span>

<span data-ttu-id="ca627-286">Následující příklad ukazuje volání `UseLazyLoadingProxies` v `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="ca627-286">The following example demonstrates calling `UseLazyLoadingProxies` in `Startup.ConfigureServices`:</span></span>

```csharp
services
    .AddDbContext<ApplicationDbContext>(
        b => b.UseSqlServer(connectionString)
              .UseLazyLoadingProxies())
    .AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

<span data-ttu-id="ca627-287">Naleznete v předchozích ukázkách pro doprovodné materiály k přidávání navigačních vlastností pro typy entit.</span><span class="sxs-lookup"><span data-stu-id="ca627-287">Refer to the preceding examples for guidance on adding navigation properties to the entity types.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca627-288">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="ca627-288">Additional resources</span></span>

* <xref:security/authentication/scaffold-identity>

::: moniker-end
