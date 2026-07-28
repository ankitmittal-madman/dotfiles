<div id="page-s{{N}}" class="page-content" style="display:none">

  <!-- ── Session header ── -->
  <div class="page-header">
    <div class="page-title">S{{N}} · {{FULL_TITLE}}</div>
    <div class="page-subtitle">{{ONE_SENTENCE_PLAIN_ENGLISH_SUMMARY}}</div>
  </div>

  <!-- ══ BEFORE / AFTER / FILES CHANGED ══
       This is the most important section for a non-technical PM.
       Always write this FIRST before any other section.
       Plain English only — no filenames in Before/After, no jargon.
       Files Changed: real paths, comma-separated, monospace.
  -->
  <div class="impact-bar">
    <div class="impact-col impact-before">
      <div class="impact-label">⛔ Before this session</div>
      <div class="impact-text">{{WHAT_USER_COULD_NOT_DO_PLAIN_ENGLISH}}</div>
    </div>
    <div class="impact-arrow">→</div>
    <div class="impact-col impact-after">
      <div class="impact-label">✅ After this session</div>
      <div class="impact-text">{{WHAT_USER_CAN_NOW_DO_PLAIN_ENGLISH}}</div>
    </div>
  </div>

  <!-- ── Files changed this session ── -->
  <div class="files-changed">
    <div class="files-changed-label">📁 Files changed this session</div>
    <div class="files-changed-list">
      {{REPEAT_FOR_EACH_FILE:
      <span class="fc-file">
        <span class="fc-path">{{FILE_PATH}}</span>
        <span class="tag {{TAG_CLASS}}">{{TAG_LABEL}}</span>
      </span>
      }}
    </div>
  </div>

  <!-- ── Summary card ── -->
  <div class="session-card">
    <div class="session-card-header">
      <div class="session-card-title">What was built this session</div>
      <div class="session-card-meta">{{DATE_FULL}}<br>{{N_THINGS}} things touched</div>
    </div>
    <div class="session-card-desc">{{2_3_SENTENCE_PLAIN_ENGLISH_DETAIL}}</div>
    <div class="stat-row">
      <div class="stat"><div class="stat-n" style="color:#1a56db">{{COUNT_SCREENS}}</div><div class="stat-l">Screen{{PLURAL}}</div></div>
      <div class="stat"><div class="stat-n" style="color:#5145b8">{{COUNT_CODE}}</div><div class="stat-l">Code files</div></div>
      <div class="stat"><div class="stat-n" style="color:#0e7a5a">{{COUNT_DB}}</div><div class="stat-l">DB change{{PLURAL}}</div></div>
      <div class="stat"><div class="stat-n" style="color:#92500a">{{COUNT_SERVER}}</div><div class="stat-l">Server fn{{PLURAL}}</div></div>
    </div>
  </div>

  <!-- ── View tabs ── -->
  <div class="view-tabs">
    <div class="view-tab active" onclick="switchView('s{{N}}','swim')">Swim lane flow</div>
    <div class="view-tab" onclick="switchView('s{{N}}','detail')">Detail drill-down</div>
  </div>

  <!-- ══ SWIM LANE VIEW ══ -->
  <div id="s{{N}}-swim" class="view-pane active">

    <!-- PHONE LANE — steps the user sees or triggers -->
    <div class="swim-lane lane-blue">
      <div class="swim-label"><div class="swim-label-inner">
        <div class="swim-label-title">Phone</div>
        <div class="swim-label-sub">user sees</div>
      </div></div>
      <div class="swim-body">
        {{REPEAT_FOR_EACH_PHONE_STEP:
        <div class="swim-step">
          <div class="step-num num-blue">{{STEP_N}}</div>
          <div class="step-content">
            <div class="step-title-row">
              <span class="step-title">{{STEP_TITLE}}</span>
              <span class="tag {{TAG_CLASS}}">{{TAG_LABEL}}</span>
            </div>
            <div class="step-desc">{{PLAIN_ENGLISH_DESCRIPTION}}</div>
          </div>
        </div>
        }}
      </div>
    </div>

    <div class="swim-arrow">↕ {{TRANSITION_DESCRIPTION}}</div>

    <!-- APP LOGIC LANE — hooks, services, business logic -->
    <div class="swim-lane" style="margin-bottom:10px">
      <div class="swim-label"><div class="swim-label-inner">
        <div class="swim-label-title">App logic</div>
        <div class="swim-label-sub">hooks / code</div>
      </div></div>
      <div class="swim-body" style="background:var(--purple-bg);border-color:var(--purple-border)">
        {{REPEAT_FOR_EACH_LOGIC_STEP: same structure as phone lane, use num-purple}}
      </div>
    </div>

    <div class="swim-arrow">↕ {{TRANSITION_DESCRIPTION}}</div>

    <!-- DATABASE LANE — tables, columns, migrations -->
    <div class="swim-lane lane-teal">
      <div class="swim-label"><div class="swim-label-inner">
        <div class="swim-label-title">Database</div>
        <div class="swim-label-sub">Supabase</div>
      </div></div>
      <div class="swim-body">
        {{REPEAT_FOR_EACH_DB_STEP: same structure, use num-teal}}
      </div>
    </div>

    <!-- Only include server lane if server functions were touched -->
    <div class="swim-arrow">↕ {{TRANSITION_DESCRIPTION}}</div>

    <!-- SERVER LANE — edge functions, cron jobs, webhooks -->
    <div class="swim-lane lane-amber">
      <div class="swim-label"><div class="swim-label-inner">
        <div class="swim-label-title">Server</div>
        <div class="swim-label-sub">edge functions</div>
      </div></div>
      <div class="swim-body">
        {{REPEAT_FOR_EACH_SERVER_STEP: same structure, use num-amber}}
      </div>
    </div>

    <!-- Next session box — always present -->
    <div class="next-box">
      <div class="next-label">Next session</div>
      <div class="next-text">{{WHAT_STILL_NEEDS_TO_BE_DONE_PLAIN_ENGLISH}}</div>
    </div>

  </div><!-- /swim -->

  <!-- ══ DETAIL DRILL-DOWN VIEW ══ -->
  <div id="s{{N}}-detail" class="view-pane">

    {{REPEAT_FOR_EACH_TOUCHED_ITEM:
    <div class="detail-item">
      <div class="detail-row" id="row-s{{N}}-{{ITEM_ID}}" onclick="toggleDetail('s{{N}}-{{ITEM_ID}}')">
        <div class="detail-left">
          <span class="tag {{TAG_CLASS}}">{{TAG_LABEL}}</span>
          <span class="detail-name {{plain_if_not_code}}">{{FILENAME_OR_ITEM_NAME}}</span>
        </div>
        <span class="detail-chevron" id="chev-s{{N}}-{{ITEM_ID}}">▾</span>
      </div>
      <div class="detail-drawer" id="draw-s{{N}}-{{ITEM_ID}}">

        <div class="seq-strip">
          <span class="seq-strip-label">Session flow</span>
          {{REPEAT_FOR_EACH_SESSION_STEP:
          <div class="seq-node">
            <div class="seq-step {{seq-active OR seq-done OR style='opacity:.4'}}"
                 onclick="gotoSwimStep('s{{N}}','{{ITEM_ID}}',{{STEP_NUM}})">
              <span class="seq-num {{seq-num-COLOR}}">{{STEP_NUM}}</span>
              {{3_WORD_MAX_LABEL}}
            </div>
            {{ADD: <span class="seq-arr">›</span> — except after the last step}}
          </div>
          }}
          <a class="seq-jump" onclick="jumpSwim('s{{N}}',{{FIRST_ACTIVE_STEP_NUM}})">View in swim lane ↗</a>
        </div>

        <div class="dd-label">What this does</div>
        <div class="dd-text">{{2_3_SENTENCES_PLAIN_ENGLISH_NO_JARGON}}</div>

        <div class="dd-label">Input → Output</div>
        <div class="dd-io">
          <div class="dd-io-col dd-io-in">
            <div class="dd-io-label">Input</div>
            <div class="dd-io-text">{{WHAT_GOES_IN_PLAIN_ENGLISH}}</div>
          </div>
          <div class="dd-io-arrow">→</div>
          <div class="dd-io-col dd-io-out">
            <div class="dd-io-label">Output</div>
            <div class="dd-io-text">{{WHAT_COMES_OUT_PLAIN_ENGLISH}}</div>
          </div>
        </div>

        <div class="dd-label">Flow through it</div>
        <div class="dd-flow">
          <span class="dd-node">{{STEP_1}}</span><span class="dd-arrow">→</span>
          <span class="dd-node">{{STEP_2}}</span><span class="dd-arrow">→</span>
          <span class="dd-node">{{STEP_N}}</span>
        </div>

        <div class="dd-label">Key line of code</div>
        <div class="dd-code"><span class="dd-hl">{{MOST_IMPORTANT_LINE}}</span>  ← {{PLAIN_ENGLISH_EXPLANATION}}</div>

        {{REPEAT_FOR_EACH_DECISION:
        <div class="dd-why">
          <div class="dd-why-q">{{DECISION_QUESTION}}</div>
          <div class="dd-why-a">{{PLAIN_ENGLISH_ANSWER_WHY_THIS_WAY}}</div>
        </div>
        }}

      </div>
    </div>
    }}

    <div class="next-box">
      <div class="next-label">Next session</div>
      <div class="next-text">{{WHAT_STILL_NEEDS_TO_BE_DONE}}</div>
    </div>

  </div><!-- /detail -->

</div><!-- /page-s{{N}} -->
