# Banking Goal-Shift Dataset Documentation

## 📋 Overview

This comprehensive banking dataset contains **120 carefully designed tasks** for evaluating conversational AI agents in banking customer service scenarios with goal shifts. The dataset covers the full spectrum of banking interactions, user personas, and goal transition patterns.

## 🏗️ Dataset Structure

### 📊 Complete Coverage Matrix

| **Component** | **Count** | **Description** |
|---------------|-----------|-----------------|
| **Total Tasks** | **120** | Complete banking goal-shift evaluation suite |
| **Original Conversions** | 15 | Hand-crafted tasks converted from action-based system |
| **Systematic Matrix** | 105 | Auto-generated using 3-pattern framework |
| **Use Cases** | 7 | Core banking service categories |
| **Personas** | 5 | Diverse user behavior profiles |
| **Goal Patterns** | 3 | Single, soft shift, hard shift variations |

### 🎯 Use Cases Covered

| **Use Case** | **Focus Area** | **Example Goals** |
|--------------|----------------|-------------------|
| **Authentication** | Identity verification | `authentication` → `account_info` → `fraud_response` |
| **Account Overview** | Balance and status checks | `account_info` → `statements` → `dispute` |
| **Bill Pay** | Payment processing | `payments` → `account_info` → `fraud_response` |
| **Card Management** | Card services and security | `cards` → `account_info` → `dispute` |
| **Fraud & Disputes** | Security and disputes | `dispute` → `fraud_response` → `cards` |
| **Transaction Review** | Activity analysis | `transactions` → `statements` → `fraud_response` |
| **Insights & Budgeting** | Financial analytics | `insights` → `statements` → `dispute` |

### 🎭 User Personas

| **Persona** | **Characteristics** | **Interaction Style** | **Tasks per Persona** |
|-------------|--------------------|-----------------------|----------------------|
| **EASY_1** | Polite, detail-oriented, step-by-step | "Please walk me through..." | 24 |
| **EASY_2** | Easily distracted, casual, confused | "Oh wait, actually..." | 24 |
| **MEDIUM_1** | Business-focused, impatient, efficient | "I need this done quickly" | 24 |
| **MEDIUM_2** | Curious learner, asks questions | "Can you teach me about..." | 24 |
| **HARD_1** | Suspicious, questioning, demands proof | "How do I know this is secure?" | 24 |

### 🔄 Goal Shift Patterns

| **Pattern** | **Goal Count** | **Shifts** | **Purpose** | **Tasks per Pattern** |
|-------------|----------------|------------|-------------|----------------------|
| **Single** | 1 | 0 | Baseline competency testing | 40 |
| **Soft Shift** | 2 | 1 | Information flow transitions | 40 |
| **Hard Shift** | 3 | 2 | Security escalation scenarios | 40 |

## 🔍 Task Structure

### Schema Overview

Each task follows the declarative goal-shift system with this structure:

```json
{
  "id": "banking_usecase_persona_pattern_001_systematic",
  "description": {
    "purpose": "Brief description of test scenario",
    "relevant_policies": "Applicable banking policies",
    "notes": "Pattern and persona details"
  },
  "user_scenario": {
    "persona": "EASY_1|EASY_2|MEDIUM_1|MEDIUM_2|HARD_1",
    "instructions": {
      "domain": "banking",
      "reason_for_call": "User's initial reason for contact",
      "known_info": "Customer details and context",
      "unknown_info": "Information user needs to discover",
      "task_instructions": "Specific scenario guidance"
    },
    "goal_shifts": {
      "required_shifts": 0|1|2,
      "goals": ["goal1", "goal2", "goal3"]
    }
  },
  "initial_state": {
    "initialization_data": {
      "agent_data": null,
      "user_data": {
        "phone_number": "+1234567890",
        "customer_id": "cust_001",
        "authenticated": false,
        // ... additional context
      }
    },
    "initialization_actions": [
      {
        "env_type": "user",
        "func_name": "update_user",
        "arguments": { /* user state setup */ }
      }
    ],
    "message_history": []
  }
}
```

### Goal Shift Logic

The dataset uses **declarative goal shifts** where:
- `required_shifts = len(goals) - 1` for multi-goal scenarios
- `required_shifts = 0` for single-goal baselines
- Goals are achieved through natural conversation flow via `BankingUserSimulator`

## 📝 Example Tasks

### Single Goal (Baseline)
```json
{
  "id": "banking_auth_easy1_single_001_systematic",
  "user_scenario": {
    "persona": "EASY_1",
    "goal_shifts": {
      "required_shifts": 0,
      "goals": ["authentication"]
    }
  }
}
```

### Soft Shift (Information Flow)
```json
{
  "id": "banking_auth_easy1_soft_001_systematic", 
  "user_scenario": {
    "persona": "EASY_1",
    "goal_shifts": {
      "required_shifts": 1,
      "goals": ["authentication", "account_info"]
    }
  }
}
```

### Hard Shift (Security Escalation)
```json
{
  "id": "banking_auth_easy1_hard_001_systematic",
  "user_scenario": {
    "persona": "EASY_1", 
    "goal_shifts": {
      "required_shifts": 2,
      "goals": ["authentication", "transactions", "fraud_response"]
    }
  }
}
```

## 🚀 Usage Guide

### Running Banking Simulations

```bash
# Run single task
tau2 run --domain banking --task-id banking_auth_easy1_soft_001_systematic

# Run all authentication tasks
tau2 run --domain banking --task-filter "banking_auth_.*"

# Run specific persona tasks  
tau2 run --domain banking --task-filter ".*_easy1_.*"

# Run pattern-specific tasks
tau2 run --domain banking --task-filter ".*_soft_.*"
```

### Task Filtering Examples

```bash
# All single-goal baselines
--task-filter ".*_single_.*"

# All hard shifts (security scenarios)
--task-filter ".*_hard_.*"

# All fraud-related tasks
--task-filter "banking_fraud_.*"

# Business user scenarios
--task-filter ".*_medium1_.*"

# Original converted tasks
--task-filter ".*_converted"
```

### Batch Evaluation

```bash
# Run representative sample (35 tasks: 5 per use case)
tau2 run --domain banking --task-filter "banking_(auth|account|billpay|cards|fraud|transactions|insights)_.*_single_001.*"

# Run persona comparison (21 tasks: 3 patterns for each persona)
tau2 run --domain banking --task-filter "banking_auth_(easy1|easy2|medium1|medium2|hard1)_.*"

# Run pattern analysis (21 tasks: authentication across all patterns/personas)  
tau2 run --domain banking --task-filter "banking_auth_.*"
```

## 🧪 Validation & Testing

### Structural Validation

All 120 tasks have been validated for:
- ✅ **Schema compliance** with tau2 declarative system
- ✅ **Goal shift logic** correctness (required_shifts calculation)
- ✅ **Customer data integrity** (consistent with banking database)
- ✅ **Persona integration** (appropriate traits and behaviors)
- ✅ **Banking context** (realistic scenarios using actual tools)

### Coverage Analysis

- **100% use case coverage**: All 7 banking service areas
- **100% persona coverage**: All 5 user behavior profiles  
- **100% pattern coverage**: Single, soft, and hard shifts
- **Balanced distribution**: ~17 tasks per use case, 24 per persona, 40 per pattern

## 🔧 Technical Details

### Customer Data Template

All tasks use consistent customer data:
```json
{
  "phone_number": "+1234567890",
  "date_of_birth": "1990-06-15",
  "email": "alex.morgan@example.com", 
  "customer_id": "cust_001",
  "primary_account_id": "acc_001",
  "primary_card_id": "card_001"
}
```

### Banking Tools Integration

Tasks leverage the complete banking toolset:
- **Authentication**: `authenticate_customer`, `send_2fa_code`
- **Account Management**: `get_customer_accounts`, `get_account_balance`
- **Payments**: `create_payment_request`, `execute_payment`
- **Card Services**: `get_customer_cards`, `lock_card`, `unlock_card`
- **Security**: `file_dispute`, `log_shift_event`
- **Analytics**: `get_spending_insights`, `get_account_statements`

### Goal Transition Patterns

| **From** | **To** | **Transition Type** | **Example Context** |
|----------|--------|-------------------|-------------------|
| `authentication` | `account_info` | Information Flow | "Now show me my balances" |
| `account_info` | `statements` | Information Flow | "Can I get recent statements?" |
| `payments` | `fraud_response` | Security Escalation | "This payment failed - is my account compromised?" |
| `transactions` | `dispute` | Security Escalation | "I don't recognize this charge" |
| `cards` | `fraud_response` | Security Escalation | "My card was stolen" |

## 📈 Research Applications

### Goal Shift Analysis

This dataset enables research into:
- **Natural goal transitions** in banking conversations
- **Persona impact** on shift behavior and success rates
- **Security escalation patterns** and agent response quality
- **Multi-turn conversation management** across banking domains

### Evaluation Metrics

Recommended metrics for analysis:
- **Goal completion rate** per pattern/persona combination
- **Transition success** for soft vs. hard shifts
- **Security response quality** in hard shift scenarios
- **Customer satisfaction** across persona types
- **Conversation length** and efficiency by pattern

### Comparative Studies

The systematic structure enables:
- **Cross-persona analysis**: How do different user types affect outcomes?
- **Pattern complexity**: Are hard shifts significantly more challenging?
- **Use case difficulty**: Which banking services are most complex?
- **Agent performance**: Which goal transitions cause most failures?

## 🔍 Quality Assurance

### Generation Method

- **Original 15 tasks**: Hand-converted from action-based system for baseline quality
- **Systematic 105 tasks**: Auto-generated using validated 3-pattern framework
- **Comprehensive validation**: 100% structural compliance verified
- **Realistic scenarios**: All use actual banking tools and customer data

### Continuous Validation

Tasks are designed to work with:
- ✅ `BankingUserSimulator` for natural goal transitions
- ✅ Banking environment tools and policies
- ✅ Customer database and realistic user data
- ✅ All agent implementations (LLM, GT, Solo)

## 🤝 Contributing

### Adding New Tasks

To extend the dataset:

1. **Follow naming convention**: `banking_usecase_persona_pattern_NNN_systematic`
2. **Use existing customer data**: Maintain consistency with `cust_001` profile
3. **Validate goal shift logic**: Ensure `required_shifts = len(goals) - 1`
4. **Test with banking tools**: Verify scenarios use actual banking capabilities
5. **Include persona traits**: Match persona characteristics in `known_info`

### Task Enhancement

For improving existing tasks:
- Update `task_instructions` for clearer scenario guidance
- Enhance `known_info` with more realistic customer context
- Refine goal transitions to be more natural
- Add edge cases or error conditions

## 📚 Related Documentation

- **Banking Domain Overview**: `data/tau2/domains/banking/README_goal_shifts.md`
- **User Personas**: `data/tau2/domains/banking/user_personas.json`
- **Banking Tools**: `data/tau2/domains/banking/tools.md`
- **Banking Policies**: `data/tau2/domains/banking/policy.md`
- **Main Project README**: `README.md`

---

**Dataset Version**: 1.0  
**Last Updated**: 2024  
**Total Tasks**: 120  
**Validation Status**: ✅ Complete  
**Production Ready**: ✅ Yes

*This dataset represents a comprehensive foundation for banking goal-shift research and conversational AI evaluation in financial services.*
