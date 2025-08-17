# Banking Dataset Quick Start Guide

## 🚀 Get Started in 5 Minutes

### What You Have
**120 banking goal-shift tasks** ready for evaluation:
- **15 hand-converted** high-quality baseline tasks
- **105 systematic** auto-generated matrix tasks  
- **Complete coverage**: 7 use cases × 5 personas × 3 patterns

### Quick Test Commands

```bash
# Test single task
tau2 run --domain banking --task-id banking_auth_easy1_single_001_systematic

# Run 5-task sample (one per persona)
tau2 run --domain banking --task-filter "banking_auth_.*(easy1|easy2|medium1|medium2|hard1)_single_001.*"

# Test all authentication flows
tau2 run --domain banking --task-filter "banking_auth_.*"
```

## 📊 Task Naming Convention

```
banking_<usecase>_<persona>_<pattern>_001_systematic
```

**Examples:**
- `banking_auth_easy1_single_001_systematic` - Simple auth with polite user
- `banking_fraud_hard1_hard_001_systematic` - Complex fraud with suspicious user  
- `banking_billpay_medium1_soft_001_systematic` - Payment + account check, business user

## 🎯 Pattern Quick Reference

| **Pattern** | **Goals** | **Use Case** |
|-------------|-----------|--------------|
| **single** | 1 goal, 0 shifts | Baseline competency |
| **soft** | 2 goals, 1 shift | Information flow |  
| **hard** | 3 goals, 2 shifts | Security escalation |

## 🎭 Persona Quick Reference

| **Persona** | **Style** | **Difficulty** |
|-------------|-----------|----------------|
| **easy1** | Polite, methodical | Low |
| **easy2** | Scattered, needs help | Low |
| **medium1** | Business, impatient | Medium |
| **medium2** | Curious, learning | Medium |
| **hard1** | Suspicious, demanding | High |

## 🔍 Common Filters

```bash
# All baselines (no goal shifts)
--task-filter ".*_single_.*"

# All complex scenarios  
--task-filter ".*_hard_.*"

# Specific persona
--task-filter ".*_medium1_.*"

# Fraud scenarios only
--task-filter "banking_fraud_.*"

# Original converted tasks
--task-filter ".*_converted"
```

## 📈 Recommended Test Sets

### Quick Validation (5 tasks)
```bash
tau2 run --domain banking --task-filter "banking_auth_(easy1|medium1|hard1)_(single|soft|hard)_001.*" --max-tasks 5
```

### Persona Comparison (15 tasks)
```bash
tau2 run --domain banking --task-filter "banking_auth_.*_001.*"
```

### Full Use Case (21 tasks)
```bash
tau2 run --domain banking --task-filter "banking_auth_.*"
```

## 🛠️ Troubleshooting

### Python Version Error
```
TypeError: unsupported operand type(s) for |: 'type' and 'type'
```
**Solution**: Requires Python 3.10+. Tasks are structurally valid - update environment when ready.

### No Tasks Found
```bash
# Check task count
tau2 domain banking --list-tasks | wc -l
# Should show 120+ tasks
```

### Runtime Issues
```bash
# Validate banking domain
tau2 check-data --domain banking
```

## 📋 Next Steps

1. **Test sample tasks** with your preferred agent
2. **Run persona analysis** to compare user behavior impact
3. **Evaluate goal-shift success** across patterns
4. **Review comprehensive documentation** in `README_banking_dataset.md`

---

**Need Help?** See full documentation in `README_banking_dataset.md` or contact the team.
