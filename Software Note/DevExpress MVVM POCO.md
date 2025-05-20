
# POCOViewModel Paradigm
Should not:
```Csharp
/// <summary>
/// Gets a value indicating whether the credit note is in lockdown
/// </summary>
[DependsOnProperties(nameof(CreditNote))]
public bool IsLockdown => CreditNote == null ||
        CreditNote.Status is NewCreditNoteStatus.Cancelled 
```

Should:
```Csharp
/// <summary>
/// Gets a value indicating whether the credit note is in lockdown
/// </summary>
[DependsOnProperties(nameof(CreditNote))]
public virtual bool IsLockdown => CreditNote == null ||
        CreditNote.Status is NewCreditNoteStatus.Cancelled
```

Reason:

A get only property would never fire changed events, neither is it virtual
#

Should not:
```Csharp
fluentApi.SetBinding(actionRibbonPageGroup, x => x.Enabled, vm => vm.!IsNotEnabled);
```

Should:
```Csharp
fluentApi.SetBinding(actionRibbonPageGroup, x => x.Enabled, vm => vm.IsEnabled);
```

Reason:
mvvm fluent api not allow Logical operations, keep UI logic inside view model

# Template to copy

Should not:
```Csharp

```

Should:
```Csharp

```

Reason: