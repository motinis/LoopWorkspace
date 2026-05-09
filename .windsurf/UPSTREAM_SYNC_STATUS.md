# Upstream Sync Status

## Last Manual Sync: 2026-05-09

### Changes Applied from upstream/dev

**Critical build fixes applied:**
- ✅ Updated all GitHub Actions workflows to use `macos-26` runners
- ✅ Updated Xcode to 26.2 (matching upstream)
- ✅ Updated GitHub Actions versions:
  - `actions/checkout@v4` → `@v5`
  - `actions/upload-artifact@v4` → `@v6`
  - `aormsby/Fork-Sync-With-Upstream-action@v3.4.1` → `@v3.4.2`
- ✅ Fixed NUKE_CERT case sensitivity issues in `create_certs.yml`

**Files modified:**
- `.github/workflows/build_loop.yml`
- `.github/workflows/add_identifiers.yml`
- `.github/workflows/create_certs.yml`
- `.github/workflows/validate_secrets.yml`

### Customizations Preserved

**Our customizations that differ from upstream:**
1. **CustomizationSelect script**: Kept in build_loop.yml
   ```bash
   /bin/bash -c "$(curl -fsSL \
   https://raw.githubusercontent.com/loopandlearn/lnl-scripts/main/CustomizationSelect.sh)" \
   future_carbs_4h \
   meal_days
   ```

### Pending Upstream Changes (Not Yet Merged)

To check what's new in upstream, run:
```bash
git fetch upstream
git log HEAD..upstream/dev --oneline -- . ':!Loop' ':!LoopKit' ':!AmplitudeService' ':!CGMBLEKit' ':!G7SensorKit' ':!LibreTransmitter' ':!LogglyService' ':!LoopOnboarding' ':!LoopSupport' ':!MinimedKit' ':!Minizip' ':!MixpanelService' ':!NightscoutRemoteCGM' ':!NightscoutService' ':!OmniBLE' ':!OmniKit' ':!RileyLinkKit' ':!TidepoolService' ':!TrueTime.swift' ':!dexcom-share-client-swift'
```

**Known pending changes:**
- Version bump: `VersionOverride.xcconfig` (13.11.1 → 3.13.1)
- Updated translation scripts
- Updated `Package.resolved` and `.gitmodules`
- Various dependency updates (Gemfile.lock, etc.)

### Next Full Merge

When ready to do a full merge:
```bash
# Create a backup branch first
git checkout -b backup-before-merge

# Return to your working branch
git checkout browser-build-3.11.x-merged

# Merge upstream (will show conflicts for customizations)
git merge upstream/dev

# Resolve conflicts, keeping your customizations
# Then commit the merge
```

### Quick Status Check

To see if you're up to date with upstream (excluding submodules):
```bash
git fetch upstream
git diff --stat HEAD..upstream/dev -- . ':!*/' # Shows changed files
```
