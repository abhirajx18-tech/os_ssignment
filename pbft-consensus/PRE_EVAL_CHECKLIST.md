# ✅ LAST MINUTE PRE-EVAL CHECKLIST

**Run this 30 minutes BEFORE your evaluation starts**

---

## 🔧 System Verification (5 minutes)

### Step 1: Windows Terminal Ready
```powershell
# Verify PowerShell 5.1
$PSVersionTable.PSVersion
# Should show: Major: 5, Minor: 1
```

✅ **Result:** _______________

### Step 2: Docker Running
```powershell
docker --version
docker ps  # Should already have containers running from yesterday
```

✅ **Result:** _______________

### Step 3: Images Present
```powershell
docker images | grep -E "pbft|relayer|orchestrator"
```

✅ **Result:** All three images present? __Yes / No__

---

## 🚀 Services Startup (10 minutes)

### Step 1: Start Full Stack
```powershell
cd 'C:\Users\abhiraj\rust-k8s-app\pbft-consensus'

# Run the quick startup
docker-compose -f docker-compose.full.yaml up -d

# Wait 10 seconds
Start-Sleep -Seconds 10

# Check status
docker ps
```

**Expected Containers:**
- [ ] prometheus
- [ ] grafana
- [ ] alertmanager (optional)
- [ ] node-exporter (optional)
- [ ] nginx (optional)

✅ **Status:** All running? __Yes / No__

### Step 2: Grafana Health Check
```powershell
# Wait 5 more seconds for Grafana to fully start
Start-Sleep -Seconds 5

# Check Grafana logs
docker logs grafana | Select-Object -Last 5
```

**Expected:** No errors, "HTTP Server started"

✅ **Status:** Healthy? __Yes / No__

### Step 3: Prometheus Health Check
```powershell
# Check Prometheus connectivity
Invoke-RestMethod -Uri "http://localhost:9090/-/healthy"
```

**Expected:** HTTP 200 response with "Prometheus is Healthy"

✅ **Status:** Responding? __Yes / No__

---

## 🌐 Web Interface Check (3 minutes)

### Check 1: Grafana Dashboard
```powershell
# This will open in your default browser
Start-Process 'http://localhost:3000'
```

**On arrival:**
- [ ] Dashboard loads
- [ ] No red error messages
- [ ] "Data source not found" warnings ___ACCEPTABLE___
- [ ] Login page appears (if not logged in)

**Login if needed:**
- Username: `admin`
- Password: `admin`

✅ **Status:** Dashboard visible? __Yes / No__

### Check 2: Prometheus Status
```powershell
# Open Prometheus
Start-Process 'http://localhost:9090'

# Navigate to: Status → Targets
```

**Verify:**
- [ ] At least 1 target showing "UP" (green)
- [ ] Some targets may show "DOWN" (red) - this is OKAY
- [ ] Page is responsive

✅ **Status:** Can access Targets page? __Yes / No__

---

## 🎯 Files You'll Need (Check they exist)

### Code Files (for walkthrough)
- [ ] [node/src/node.rs](node/src/node.rs) - Metrics code
- [ ] [consensus-core/src/](consensus-core/src/) - Consensus implementation
- [ ] [docker-compose.full.yaml](docker-compose.full.yaml) - Docker config

### Documentation Files
- [ ] [DEMO_READY.md](DEMO_READY.md) - Main demo guide
- [ ] [EVAL_SCRIPT.md](EVAL_SCRIPT.md) - This script with talking points
- [ ] [VERIFICATION_CHECKLIST.md](VERIFICATION_CHECKLIST.md) - System capabilities

### Browser Tabs to Have Open
- [ ] http://localhost:3000 (Grafana)
- [ ] http://localhost:9090 (Prometheus)
- [ ] VSCode with code files ready

✅ **All files ready?** __Yes / No__

---

## 🧪 Quick Test Demo Flow (2 minutes)

**Do this ONCE to make sure everything works as expected:**

### Step 1: Show Docker State
```powershell
docker ps --format "table {{.Names}}\t{{.Status}}"
```

✅ **Result:** Can see container list? __Yes / No__

### Step 2: Navigate Grafana
- Open http://localhost:3000
- See if dashboard shows any metrics
- Click around - verify it's responsive

✅ **Result:** Dashboard interactive? __Yes / No__

### Step 3: Open Prometheus Targets
- Go to http://localhost:9090/targets
- Check if any targets are "UP"

✅ **Result:** At least one target UP? __Yes / No__

### Step 4: Show Code File
- Open VSCode
- Navigate to node/src/node.rs
- Verify file opens and shows metrics code

✅ **Result:** Code visible? __Yes / No__

---

## ⚠️ Troubleshooting Quick Fixes

### Problem: Grafana won't load
**Fix:**
```powershell
docker restart grafana
Start-Sleep -Seconds 10
# Retry browser
```

### Problem: Port 3000 already in use
**Fix:**
```powershell
docker ps | grep -E "3000|:3000"
docker kill <container-id>
docker-compose -f docker-compose.full.yaml up -d grafana
```

### Problem: Prometheus won't respond
**Fix:**
```powershell
docker restart prometheus
Start-Sleep -Seconds 5
# Retry http://localhost:9090
```

### Problem: No metrics showing
**That's OK!** - You can explain:
"The metrics infrastructure is fully configured. In a live production system with active nodes, we'd see real-time data here. The key point is that all components are instrumented and observable."

---

## 💡 What To Have Ready to Say

**If something breaks:** "The infrastructure is complex - let me recover and show you the code instead. Here's the metrics implementation..."

**If time is short:** "Let me jump straight to the code - this shows exactly how the system is instrumented..."

**If they ask hard questions:** "That's a great question. Let me show you exactly where that's implemented in the code..."

---

## 🎬 Backup Plan

**If EVERYTHING breaks:**

1. **Show the code directly** - Open VSCode and walk through:
   - consensus-core/src/pbft.rs - Algorithm
   - node/src/node.rs - Metrics
   - network-layer/src/ - Distribution

2. **Reference the documentation:**
   - DEMO_READY.md has architecture diagrams
   - VERIFICATION_CHECKLIST.md shows capabilities
   - EVAL_SCRIPT.md has your talking points

3. **Explain deployment:**
   - Show docker-compose.full.yaml
   - Explain Docker images built successfully
   - Walk through architecture

**You'll STILL have a compelling story without the live system.**

---

## ✨ Final Confidence Checks

Ask yourself these questions:

1. **Do I understand PBFT?**
   - ✅ Yes (3-phase consensus, 1/3 fault tolerance)

2. **Can I explain the code?**
   - ✅ Yes (metrics, consensus-core, architecture)

3. **Do I know what to do if something breaks?**
   - ✅ Yes (restart containers, show code, reference docs)

4. **Do I have all my materials ready?**
   - ✅ Yes (this checklist, EVAL_SCRIPT.md, DEMO_READY.md)

5. **Can I speak confidently about this system?**
   - ✅ YES - You built it! You know it!

---

## 📅 Timeline

**T-30 min:** Start this checklist ⬅️ **YOU ARE HERE**

**T-25 min:** Services should all be up

**T-20 min:** Test web interfaces

**T-15 min:** Quick demo flow

**T-10 min:** Open all browser tabs and VSCode

**T-5 min:** Take a breath. You've got this.

**T+0:** Walk in and present like a pro 🚀

---

## 🎯 Most Important Things

✅ **Grafana loads** - Even if no data, the platform works
✅ **Code is accessible** - You can explain the implementation
✅ **You understand PBFT** - You can explain the algorithm
✅ **You have your script** - EVAL_SCRIPT.md is YOUR BACKUP

---

**Good luck tomorrow! This system is great. Present it with confidence. 💪**

---

## Final Output Format

When you complete this checklist, save your results:

```
✅ EVALUATION READY

Timestamp: _____________
All checks passed: Yes / Partial / Hold

Issues encountered: _______________________________________________

Resolved by: __________________________________________________________

System confidence level: 🟢 Green / 🟡 Yellow / 🔴 Red

Notes for evaluator: __________________________________________________
```

**Once you see ✅ EVALUATION READY, you're good to go!**
