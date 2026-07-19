# Validation.FluentValidation — DEPRECATED

> ## ⛔ DEPRECATED — do not install. Use [`DLoizides.Validation`](https://github.com/openmindednewby/DLoizides.Validation) instead.
>
> This package is a **duplicate**. Its five source files are byte-identical to those of
> `DLoizides.Validation` apart from the namespace token and a UTF-8 BOM; the `<Description>`
> string is verbatim identical. The two packages were published in parallel by accident.
>
> **`DLoizides.Validation` is the canonical package** and the one the fleet actually uses:
> 9 services plus 1 test project reference it. **Zero projects reference this package** — it
> reached 1.0.3 without ever having a consumer.
>
> Migration, if you somehow depend on this: replace the package reference with
> `DLoizides.Validation` and change `using Validation.FluentValidation.*` to
> `using Validation.Defaults.*`. Nothing else differs.
>
> Verified 2026-07-19 by a repo-wide sweep of every `.csproj` and `Directory.Packages.props`.

## Installation

```bash
# Don't. Install the canonical package instead:
dotnet add package DLoizides.Validation
```

## Usage

### Validation Extensions

```csharp
using FluentValidation;
using Validation.FluentValidation.Rules;

public class CreateMenuValidator : AbstractValidator<CreateMenuRequest>
{
    public CreateMenuValidator()
    {
        RuleFor(x => x.Id).NotEmptyGuid();
        RuleFor(x => x.Name).NotEmpty().MaximumLength(ValidationLimits.MaxNameLength);
        RuleFor(x => x.Color).ValidHexColor();
        RuleFor(x => x.Url).ValidUrl();
        RuleFor(x => x.Page).ValidPageNumber();
        RuleFor(x => x.PageSize).ValidPageSize();
    }
}
```

### Available Extensions

| Extension | Description |
|-----------|-------------|
| `.NotEmptyGuid()` | Rejects `Guid.Empty` |
| `.ValidHexColor()` | Accepts `#RGB`, `#RRGGBB`, `#RRGGBBAA` |
| `.ValidUrl()` | Validates well-formed HTTP/HTTPS URLs |
| `.ValidEmail()` | Validates email format |
| `.ValidPageNumber()` | Page >= 1 |
| `.ValidPageSize()` | 1 <= pageSize <= 100 |
| `.ValidSkip()` | skip >= 0 |

### Constants

```csharp
using Validation.FluentValidation.Constants;

// Field length limits
ValidationLimits.MaxNameLength        // 200
ValidationLimits.MaxDescriptionLength // 2000
ValidationLimits.MaxUrlLength         // 2048
ValidationLimits.MaxEmailLength       // 254
ValidationLimits.MaxPhoneLength       // 20
ValidationLimits.MaxColorLength       // 9 (#RRGGBBAA)
ValidationLimits.MaxPageSize          // 100
```
