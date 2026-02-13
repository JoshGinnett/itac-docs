---
hide:
  - toc
---

# Cold Air Intake



Using cold outdoor air for compressor intake instead of warm indoor air reduces compressor energy consumption. Air density increases as temperature decreases, meaning cooler intake air requires less compression work to reach target discharge pressure. This measure is most effective in climates with significant outdoor temperature variation throughout the year.

**ARC Code(s):**

## Technical Background

Compressed air systems draw ambient air, compress it to system pressure, and deliver it to end uses. The thermodynamic compression process follows the ideal gas relationship where compression work is proportional to inlet air temperature. Lower inlet temperature results in lower compression work for the same mass flow and discharge pressure.

Most industrial facilities locate compressors indoors for weather protection and maintenance accessibility. Indoor temperatures typically exceed outdoor temperatures due to facility heating, process heat gains, and compressor waste heat. Redirecting compressor intake from indoor air to outdoor air through ducting or intake louvers reduces inlet temperature and compression work.

The measure requires analysis of monthly temperature variations to quantify annual energy savings. Demand savings depend on the compressor operating profile during facility peak demand periods.

## Calculation Methodology

Energy savings from cold air intake are calculated using thermodynamic compression principles. The isentropic (ideal) compression work depends on inlet air temperature, pressure ratio, and mass flow rate.

### Isentropic Compression Work

The ideal compression work for air is:

$$
W_{\text{ideal}} = \dot{m} \times c_p \times T_1 \times \left[ \left( \frac{P_2}{P_1} \right)^{\frac{\gamma - 1}{\gamma}} - 1 \right]
$$

Alternatively, using the specific gas constant for air:

$$
W_{\text{ideal}} = \frac{\gamma}{\gamma - 1} \times R \times T_1 \times \dot{m} \times \left[ \left( \frac{P_2}{P_1} \right)^{\frac{\gamma - 1}{\gamma}} - 1 \right]
$$

Where:

- $W_{\text{ideal}}$ = ideal compression power (kW)
- $\dot{m}$ = mass flow rate of air (kg/s)
- $c_p$ = specific heat of air at constant pressure = 1.005 kJ/(kg·K)
- $R$ = specific gas constant for air = 0.287 kJ/(kg·K)
- $T_1$ = inlet air temperature (K)
- $P_1$ = inlet pressure, typically atmospheric = 101.325 kPa
- $P_2$ = discharge pressure (kPa absolute)
- $\gamma$ = ratio of specific heats for air = 1.40

### Real Compression Power

Actual compressor power accounts for isentropic efficiency:

$$
W_{\text{actual}} = \frac{W_{\text{ideal}}}{\eta_{\text{isentropic}}}
$$

Where:

- $\eta_{\text{isentropic}}$ = isentropic efficiency from CAGI datasheet (decimal)

CAGI (Compressed Air and Gas Institute) datasheets provide standardized performance data including isentropic efficiency at rated conditions. Typical values range from 0.70 to 0.85 for rotary screw compressors.

### Monthly Energy Calculation

Calculate compression power separately for each month using monthly average outdoor temperature for the cold intake case and constant indoor temperature for the baseline case:

1. Convert volumetric flow (CFM) to mass flow using standard air density (1.225 kg/m³ at 15°C and 101.325 kPa)
2. Calculate ideal compression power for baseline (indoor temperature) and each month (outdoor temperature)
3. Calculate actual power from isentropic efficiency
4. Multiply monthly power savings by monthly operating hours to get energy savings

$$
\Delta E_{\text{month}} = (W_{\text{indoor}} - W_{\text{outdoor,month}}) \times H_{\text{month}}
$$

Where:

- $H_{\text{month}}$ = compressor loaded operating hours in the month
- Hours are allocated proportionally by days in each month

Annual energy savings sum all monthly values.

!!! note "Operating Hours Definition"

    Use loaded operating hours, not total runtime. Loaded hours represent time when the compressor is actively compressing air at design pressure. Unloaded time (motor running but intake valve closed) and off time should be excluded. This differs from total runtime for load/unload controlled compressors.

### Demand Savings

Peak demand reduction occurs when cold air intake reduces compressor power during facility peak demand periods. Calculate monthly demand savings as the power reduction in each month:

$$
\Delta kW_{\text{month}} = W_{\text{indoor}} - W_{\text{outdoor,month}}
$$

Annual demand savings in kW-months:

$$
\Delta kW\text{-months} = \sum_{\text{all months}} \Delta kW_{\text{month}}
$$

!!! warning "Seasonal Demand Variation"

    Demand savings vary significantly by month. Summer months typically show minimal or negative savings (outdoor temperature may exceed indoor temperature). Winter months provide maximum savings. Total annual demand savings account for this seasonal variation.

### Cost Savings

Total annual cost savings combine energy and demand components:

$$
\text{Annual Savings} = (\Delta E_{\text{annual}} \times \text{Energy Rate}) + (\Delta kW\text{-months} \times \text{Demand Rate})
$$

Where:

- Energy Rate = $/kWh
- Demand Rate = $/kW-month

## Anticipated Costs

Implementation costs for cold air intake include:

- **Intake ducting and louvers**: Material and installation costs for outdoor air intake path. Duct sizing should minimize pressure drop (typically < 0.5 psi).
- **Filtration**: Outdoor air may require enhanced filtration compared to indoor air to prevent contamination from pollen, dust, or other environmental particles.
- **Freeze protection**: In cold climates, intake dampers or heating elements may be required to prevent freezing of compressor components or condensate systems.
- **Controls**: Automatic dampers or controls to switch between indoor and outdoor intake based on temperature or for backup during extreme weather.

Simple payback periods typically range from 1 to 4 years depending on:

- Indoor-outdoor temperature differential (larger differential = shorter payback)
- Compressor operating hours (higher utilization = shorter payback)
- Energy and demand rates (higher rates = shorter payback)
- Installation complexity (longer duct runs or structural modifications increase cost)

Facilities in northern climates with high indoor temperatures (due to process heat or inadequate ventilation) realize the greatest savings. Facilities in mild climates or with low indoor temperatures may see minimal benefit.

---

## Interactive Cold Air Intake Calculator

Use this calculator to estimate energy and cost savings from implementing a cold air intake system. Enter your compressor parameters, monthly outdoor temperatures, and utility rates to see detailed monthly savings analysis.

<div id="cold-air-calculator" style="max-width: 1200px; margin: 20px auto; padding: 20px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 8px; background: var(--md-code-bg-color);">

<h3>Compressor Parameters</h3>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 20px 0;">
    <div>
        <label for="flowRate" style="display: block; margin-bottom: 5px; font-weight: 500;">Air Flow Rate (CFM):</label>
        <input type="number" id="flowRate" value="447" step="1" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="dischargePressure" style="display: block; margin-bottom: 5px; font-weight: 500;">Discharge Pressure (PSI):</label>
        <input type="number" id="dischargePressure" value="145" step="1" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
</div>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 20px 0;">
    <div>
        <label for="isentropicEff" style="display: block; margin-bottom: 5px; font-weight: 500;">CAGI Isentropic Efficiency (%):</label>
        <input type="number" id="isentropicEff" value="78.61" step="0.01" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="indoorTemp" style="display: block; margin-bottom: 5px; font-weight: 500;">Indoor Temperature (Current Intake) (°C):</label>
        <input type="number" id="indoorTemp" value="31.93" step="0.1" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
</div>

<div style="margin: 20px 0;">
    <label for="annualHours" style="display: block; margin-bottom: 5px; font-weight: 500;">Annual Loaded Operating Hours:</label>
    <input type="number" id="annualHours" value="3650" step="1" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;">Hours when compressor is actively producing compressed air (excludes unloaded/idle time)</p>
</div>

<h3 style="margin-top: 30px;">Cost Parameters</h3>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 20px 0;">
    <div>
        <label for="electricRate" style="display: block; margin-bottom: 5px; font-weight: 500;">Energy Rate ($/kWh):</label>
        <input type="number" id="electricRate" value="0.12" step="0.01" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="demandRate" style="display: block; margin-bottom: 5px; font-weight: 500;">Demand Rate ($/kW-month):</label>
        <input type="number" id="demandRate" value="8.50" step="0.01" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;">Monthly demand charge per kW of peak demand</p>
    </div>
</div>

<h3 style="margin-top: 30px;">Monthly Outdoor Temperatures</h3>

<div style="margin: 15px 0;">
    <label style="display: block; margin-bottom: 10px; font-weight: 500;">Location Preset:</label>
    <div style="display: flex; gap: 10px; flex-wrap: wrap;">
        <button onclick="setLocation('ct')" style="padding: 8px 16px; background: var(--md-default-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; cursor: pointer; color: var(--md-default-fg-color);">Connecticut</button>
        <button onclick="setLocation('me')" style="padding: 8px 16px; background: var(--md-default-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; cursor: pointer; color: var(--md-default-fg-color);">Maine</button>
        <button onclick="setLocation('tx')" style="padding: 8px 16px; background: var(--md-default-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; cursor: pointer; color: var(--md-default-fg-color);">Texas</button>
        <button onclick="setLocation('ca')" style="padding: 8px 16px; background: var(--md-default-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; cursor: pointer; color: var(--md-default-fg-color);">California</button>
    </div>
</div>

<p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin: 10px 0;">Average monthly outdoor temperatures (°C):</p>

<div style="display: grid; grid-template-columns: repeat(6, 1fr); gap: 10px; margin: 15px 0;">
    <div>
        <label for="temp1" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Jan</label>
        <input type="number" id="temp1" value="-8.3" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp2" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Feb</label>
        <input type="number" id="temp2" value="-1" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp3" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Mar</label>
        <input type="number" id="temp3" value="3" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp4" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Apr</label>
        <input type="number" id="temp4" value="9" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp5" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">May</label>
        <input type="number" id="temp5" value="15" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp6" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Jun</label>
        <input type="number" id="temp6" value="20" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp7" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Jul</label>
        <input type="number" id="temp7" value="23" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp8" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Aug</label>
        <input type="number" id="temp8" value="22" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp9" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Sep</label>
        <input type="number" id="temp9" value="18" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp10" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Oct</label>
        <input type="number" id="temp10" value="11" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp11" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Nov</label>
        <input type="number" id="temp11" value="6" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="temp12" style="display: block; margin-bottom: 5px; font-size: 0.85em; text-align: center;">Dec</label>
        <input type="number" id="temp12" value="1" step="0.1" style="width: 100%; padding: 6px; text-align: center; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
</div>

<div style="margin: 20px 0; padding: 15px; background: var(--md-default-bg-color); border-left: 3px solid var(--md-accent-fg-color); border-radius: 4px;">
    <p style="margin: 0; font-size: 0.85em; color: var(--md-default-fg-color--light);"><strong>Note:</strong> This calculator assumes a fixed-speed (load/unload) compressor operating at constant output during loaded hours. VSD compressors require additional considerations for part-load efficiency curves.</p>
</div>

<h3 style="margin-top: 30px;">Results Summary</h3>

<div id="results" style="margin: 20px 0; padding: 20px; background: var(--md-default-bg-color); border-radius: 6px; border: 1px solid var(--md-default-fg-color--lightest);">
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
        <div>
            <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.9em;">Mass Flow Rate:</p>
            <p style="margin: 5px 0; font-family: monospace; font-size: 1.1em;" id="massFlowResult">0.258 kg/s</p>
        </div>
        <div>
            <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.9em;">Base Power (Indoor Intake):</p>
            <p style="margin: 5px 0; font-family: monospace; font-size: 1.1em;" id="basePowerResult">93.5 kW</p>
        </div>
    </div>

    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
        <div>
            <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.9em;">Annual Energy (Base Case):</p>
            <p style="margin: 5px 0; font-family: monospace; font-size: 1.1em;" id="baseEnergyResult">341,424 kWh</p>
        </div>
        <div>
            <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.9em;">Annual Energy (Cold Intake):</p>
            <p style="margin: 5px 0; font-family: monospace; font-size: 1.1em;" id="newEnergyResult">315,784 kWh</p>
        </div>
    </div>

    <div style="margin-top: 30px; padding: 20px; background: rgba(76, 175, 80, 0.1); border: 1px solid rgba(76, 175, 80, 0.3); border-radius: 6px;">
        <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 20px; text-align: center;">
            <div>
                <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px;">Energy Savings</p>
                <p style="margin: 5px 0; font-family: monospace; font-size: 1.4em; font-weight: 600; color: #4caf50;" id="energySavingsResult">25,640 kWh</p>
                <p style="margin: 5px 0; font-family: monospace; font-size: 1.1em; color: #4caf50;" id="energyCostResult">$3,077</p>
            </div>
            <div>
                <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px;">Demand Savings</p>
                <p style="margin: 5px 0; font-family: monospace; font-size: 1.4em; font-weight: 600; color: #4caf50;" id="demandSavingsResult">91.2 kW-mo</p>
                <p style="margin: 5px 0; font-family: monospace; font-size: 1.1em; color: #4caf50;" id="demandCostResult">$775</p>
            </div>
            <div>
                <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px;">Total Annual Savings</p>
                <p style="margin: 5px 0; font-family: monospace; font-size: 1.4em; font-weight: 600; color: #4caf50;" id="totalSavingsResult">$3,852</p>
            </div>
        </div>
    </div>
</div>

<h3 style="margin-top: 30px;">Monthly Breakdown</h3>

<div style="overflow-x: auto; margin: 20px 0;">
    <table id="resultsTable" style="width: 100%; border-collapse: collapse; font-size: 0.85em; font-family: monospace;">
        <thead>
            <tr>
                <th rowspan="2" style="padding: 10px; text-align: left; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">Month</th>
                <th colspan="2" style="padding: 10px; text-align: center; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">Physical Parameters</th>
                <th colspan="3" style="padding: 10px; text-align: center; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">Power (kW)</th>
                <th colspan="3" style="padding: 10px; text-align: center; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">Energy (kWh)</th>
            </tr>
            <tr>
                <th style="padding: 8px; text-align: right; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">T (K)</th>
                <th style="padding: 8px; text-align: right; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">Hours</th>
                <th style="padding: 8px; text-align: right; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">Ideal</th>
                <th style="padding: 8px; text-align: right; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">Real</th>
                <th style="padding: 8px; text-align: right; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest); color: #4caf50;">ΔkW</th>
                <th style="padding: 8px; text-align: right; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">Base</th>
                <th style="padding: 8px; text-align: right; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">New</th>
                <th style="padding: 8px; text-align: right; background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest); color: #4caf50;">Savings</th>
            </tr>
        </thead>
        <tbody id="tableBody">
            <!-- Populated by JavaScript -->
        </tbody>
    </table>
</div>

<div style="margin-top: 20px;">
    <button onclick="toggleLatex()" id="latexToggle" style="padding: 10px 20px; background: var(--md-default-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; cursor: pointer; color: var(--md-default-fg-color); margin-right: 10px;">Show LaTeX Table</button>
    <button onclick="copyLatex()" id="copyButton" style="padding: 10px 20px; background: var(--md-primary-fg-color); color: white; border: none; border-radius: 4px; cursor: pointer; display: none;">Copy to Clipboard</button>
</div>

<div id="latexContent" style="display: none; margin-top: 15px; padding: 15px; background: var(--md-code-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; overflow-x: auto;">
    <pre id="latexCode" style="margin: 0; font-family: monospace; font-size: 0.75em; color: var(--md-default-fg-color--light); white-space: pre;"></pre>
</div>

<div style="margin-top: 20px;">
    <button onclick="toggleEquations()" id="equationsToggle" style="padding: 10px 20px; background: var(--md-default-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; cursor: pointer; color: var(--md-default-fg-color); margin-right: 10px;">Show LaTeX Equations</button>
    <button onclick="copyEquations()" id="copyEquationsButton" style="padding: 10px 20px; background: var(--md-primary-fg-color); color: white; border: none; border-radius: 4px; cursor: pointer; display: none;">Copy to Clipboard</button>
</div>

<div id="equationsContent" style="display: none; margin-top: 15px; padding: 15px; background: var(--md-code-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; overflow-x: auto;">
    <pre id="equationsCode" style="margin: 0; font-family: monospace; font-size: 0.75em; color: var(--md-default-fg-color--light); white-space: pre;"></pre>
</div>

</div>

<script>
// Physical constants
const GAMMA = 1.40287268;
const R_AIR = 0.28703905;
const P_ATM = 101.325;
const CFM_TO_KGS = 0.000472 * 1.225;

const MONTHS = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
const DAYS_IN_MONTH = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];

const LOCATIONS = {
    ct: [-8.3, -1, 3, 9, 15, 20, 23, 22, 18, 11, 6, 1],
    me: [-8.3, -1, 3, 9, 15, 20, 23, 22, 18, 11, 6, 1],
    tx: [8, 11, 15, 20, 24, 28, 30, 30, 26, 20, 14, 9],
    ca: [10, 12, 13, 15, 17, 20, 22, 22, 21, 18, 14, 10]
};

function setLocation(loc) {
    const temps = LOCATIONS[loc];
    for (let i = 0; i < 12; i++) {
        document.getElementById(`temp${i + 1}`).value = temps[i];
    }
    calculate();
}

function celsiusToKelvin(c) {
    return c + 273.15;
}

function psiToKpa(psi) {
    return psi * 6.894757;
}

function calculateIdealPower(T_kelvin, P_discharge_kpa, massFlow) {
    const exponent = (GAMMA - 1) / GAMMA;
    const pressureRatio = P_discharge_kpa / P_ATM;
    const idealWork = (GAMMA * R_AIR * T_kelvin / (GAMMA - 1)) *
                     (Math.pow(pressureRatio, exponent) - 1) *
                     massFlow;
    return idealWork;
}

function calculateRealPower(idealPower, efficiency) {
    return idealPower / (efficiency / 100);
}

function formatNumber(num, decimals = 0) {
    return num.toLocaleString('en-US', {
        minimumFractionDigits: decimals,
        maximumFractionDigits: decimals
    });
}

let calculationResults = null;

function calculate() {
    const flowCFM = parseFloat(document.getElementById('flowRate').value);
    const dischargePSI = parseFloat(document.getElementById('dischargePressure').value);
    const efficiency = parseFloat(document.getElementById('isentropicEff').value);
    const indoorTempC = parseFloat(document.getElementById('indoorTemp').value);
    const annualHours = parseFloat(document.getElementById('annualHours').value);
    const electricRate = parseFloat(document.getElementById('electricRate').value);
    const demandRate = parseFloat(document.getElementById('demandRate').value);

    const monthlyTempsC = [];
    for (let i = 1; i <= 12; i++) {
        monthlyTempsC.push(parseFloat(document.getElementById(`temp${i}`).value));
    }

    const massFlow = flowCFM * CFM_TO_KGS;
    const dischargeKpa = psiToKpa(dischargePSI);
    const indoorTempK = celsiusToKelvin(indoorTempC);

    const baseIdealPower = calculateIdealPower(indoorTempK, dischargeKpa, massFlow);
    const baseRealPower = calculateRealPower(baseIdealPower, efficiency);

    const totalDays = DAYS_IN_MONTH.reduce((a, b) => a + b, 0);
    const monthlyHours = DAYS_IN_MONTH.map(days => (days / totalDays) * annualHours);

    const monthlyData = [];
    let totalBaseEnergy = 0;
    let totalNewEnergy = 0;
    let totalIdealPower = 0;
    let totalRealPower = 0;
    let totalDeltaKW = 0;

    for (let i = 0; i < 12; i++) {
        const tempK = celsiusToKelvin(monthlyTempsC[i]);
        const idealPower = calculateIdealPower(tempK, dischargeKpa, massFlow);
        const realPower = calculateRealPower(idealPower, efficiency);
        const hours = monthlyHours[i];
        const baseEnergy = baseRealPower * hours;
        const newEnergy = realPower * hours;
        const energySavings = baseEnergy - newEnergy;
        const deltaKW = baseRealPower - realPower;

        monthlyData.push({
            month: MONTHS[i],
            tempK: tempK,
            hours: hours,
            idealPower: idealPower,
            realPower: realPower,
            deltaKW: deltaKW,
            baseEnergy: baseEnergy,
            newEnergy: newEnergy,
            energySavings: energySavings
        });

        totalBaseEnergy += baseEnergy;
        totalNewEnergy += newEnergy;
        totalIdealPower += idealPower;
        totalRealPower += realPower;
        totalDeltaKW += deltaKW;
    }

    const totalEnergySavings = totalBaseEnergy - totalNewEnergy;
    const energyCostSavings = totalEnergySavings * electricRate;
    const demandCostSavings = totalDeltaKW * demandRate;
    const totalCostSavings = energyCostSavings + demandCostSavings;

    calculationResults = {
        monthlyData: monthlyData,
        totals: {
            hours: annualHours,
            idealPower: totalIdealPower,
            realPower: totalRealPower,
            deltaKW: totalDeltaKW,
            baseEnergy: totalBaseEnergy,
            newEnergy: totalNewEnergy,
            energySavings: totalEnergySavings
        },
        baseRealPower: baseRealPower
    };

    document.getElementById('massFlowResult').textContent = `${massFlow.toFixed(6)} kg/s`;
    document.getElementById('basePowerResult').textContent = `${baseRealPower.toFixed(2)} kW`;
    document.getElementById('baseEnergyResult').textContent = `${formatNumber(totalBaseEnergy)} kWh`;
    document.getElementById('newEnergyResult').textContent = `${formatNumber(totalNewEnergy)} kWh`;
    document.getElementById('energySavingsResult').textContent = `${formatNumber(totalEnergySavings)} kWh`;
    document.getElementById('energyCostResult').textContent = `$${formatNumber(energyCostSavings)}`;
    document.getElementById('demandSavingsResult').textContent = `${formatNumber(totalDeltaKW, 1)} kW-mo`;
    document.getElementById('demandCostResult').textContent = `$${formatNumber(demandCostSavings)}`;
    document.getElementById('totalSavingsResult').textContent = `$${formatNumber(totalCostSavings)}`;

    const tableBody = document.getElementById('tableBody');
    tableBody.innerHTML = '';

    for (const data of monthlyData) {
        const row = document.createElement('tr');
        row.innerHTML = `
            <td style="padding: 8px; border-bottom: 1px solid var(--md-default-fg-color--lightest);">${data.month}</td>
            <td style="padding: 8px; text-align: right; border-bottom: 1px solid var(--md-default-fg-color--lightest);">${data.tempK.toFixed(2)}</td>
            <td style="padding: 8px; text-align: right; border-bottom: 1px solid var(--md-default-fg-color--lightest);">${data.hours.toFixed(2)}</td>
            <td style="padding: 8px; text-align: right; border-bottom: 1px solid var(--md-default-fg-color--lightest);">${data.idealPower.toFixed(2)}</td>
            <td style="padding: 8px; text-align: right; border-bottom: 1px solid var(--md-default-fg-color--lightest);">${data.realPower.toFixed(2)}</td>
            <td style="padding: 8px; text-align: right; border-bottom: 1px solid var(--md-default-fg-color--lightest); color: #4caf50;">${data.deltaKW.toFixed(2)}</td>
            <td style="padding: 8px; text-align: right; border-bottom: 1px solid var(--md-default-fg-color--lightest);">${formatNumber(data.baseEnergy, 2)}</td>
            <td style="padding: 8px; text-align: right; border-bottom: 1px solid var(--md-default-fg-color--lightest);">${formatNumber(data.newEnergy, 2)}</td>
            <td style="padding: 8px; text-align: right; border-bottom: 1px solid var(--md-default-fg-color--lightest); color: #4caf50;">${formatNumber(data.energySavings, 2)}</td>
        `;
        tableBody.appendChild(row);
    }

    const totalRow = document.createElement('tr');
    totalRow.innerHTML = `
        <td style="padding: 10px; border-top: 2px solid var(--md-default-fg-color--lightest); font-weight: 600;">Cumulative</td>
        <td style="padding: 10px; text-align: right; border-top: 2px solid var(--md-default-fg-color--lightest); font-weight: 600;"></td>
        <td style="padding: 10px; text-align: right; border-top: 2px solid var(--md-default-fg-color--lightest); font-weight: 600;">${formatNumber(annualHours, 2)}</td>
        <td style="padding: 10px; text-align: right; border-top: 2px solid var(--md-default-fg-color--lightest); font-weight: 600;">${totalIdealPower.toFixed(2)}</td>
        <td style="padding: 10px; text-align: right; border-top: 2px solid var(--md-default-fg-color--lightest); font-weight: 600;">${totalRealPower.toFixed(2)}</td>
        <td style="padding: 10px; text-align: right; border-top: 2px solid var(--md-default-fg-color--lightest); font-weight: 600; color: #4caf50;">${totalDeltaKW.toFixed(2)}</td>
        <td style="padding: 10px; text-align: right; border-top: 2px solid var(--md-default-fg-color--lightest); font-weight: 600;">${formatNumber(totalBaseEnergy, 2)}</td>
        <td style="padding: 10px; text-align: right; border-top: 2px solid var(--md-default-fg-color--lightest); font-weight: 600;">${formatNumber(totalNewEnergy, 2)}</td>
        <td style="padding: 10px; text-align: right; border-top: 2px solid var(--md-default-fg-color--lightest); font-weight: 600; color: #4caf50;">${formatNumber(totalEnergySavings, 2)}</td>
    `;
    tableBody.appendChild(totalRow);

    generateLatex();
}

function generateLatex() {
    if (!calculationResults) return;

    const { monthlyData, totals } = calculationResults;

    let latex = `\\begin{table}[htbp]
\\centering
\\caption{Cold Air Intake Energy Savings Analysis}
\\label{tab:cold-air-intake}
\\begin{tabular}{@{}lrrrrrrrrr@{}}
\\toprule
 & \\multicolumn{2}{c}{Physical Parameters} & \\multicolumn{3}{c}{Power (kW)} & \\multicolumn{3}{c}{Energy (kWh)} \\\\
\\cmidrule(lr){2-3} \\cmidrule(lr){4-6} \\cmidrule(lr){7-9}
Month & T (K) & Hours & Ideal & Real & $\\Delta$kW & Base & New & Savings \\\\
\\midrule
`;

    for (const data of monthlyData) {
        latex += `${data.month} & ${data.tempK.toFixed(2)} & ${data.hours.toFixed(2)} & ${data.idealPower.toFixed(1)} & ${data.realPower.toFixed(2)} & ${data.deltaKW.toFixed(2)} & ${formatNumber(data.baseEnergy, 2)} & ${formatNumber(data.newEnergy, 2)} & ${formatNumber(data.energySavings, 2)} \\\\\n`;
    }

    latex += `\\midrule
Cumulative & & ${formatNumber(totals.hours, 2)} & ${totals.idealPower.toFixed(1)} & ${totals.realPower.toFixed(2)} & ${totals.deltaKW.toFixed(2)} & ${formatNumber(totals.baseEnergy, 2)} & ${formatNumber(totals.newEnergy, 2)} & ${formatNumber(totals.energySavings, 2)} \\\\
\\bottomrule
\\end{tabular}
\\end{table}`;

    document.getElementById('latexCode').textContent = latex;
}

function toggleLatex() {
    const content = document.getElementById('latexContent');
    const button = document.getElementById('latexToggle');
    const copyButton = document.getElementById('copyButton');

    if (content.style.display === 'none') {
        content.style.display = 'block';
        button.textContent = 'Hide LaTeX Table';
        copyButton.style.display = 'inline-block';
    } else {
        content.style.display = 'none';
        button.textContent = 'Show LaTeX Table';
        copyButton.style.display = 'none';
    }
}

function copyLatex() {
    const latexCode = document.getElementById('latexCode').textContent;
    const btn = document.getElementById('copyButton');

    if (navigator.clipboard && window.isSecureContext) {
        navigator.clipboard.writeText(latexCode).then(() => {
            showCopySuccess(btn);
        }).catch(() => {
            fallbackCopy(latexCode, btn);
        });
    } else {
        fallbackCopy(latexCode, btn);
    }
}

function fallbackCopy(text, btn) {
    const textArea = document.createElement('textarea');
    textArea.value = text;
    textArea.style.position = 'fixed';
    textArea.style.left = '-9999px';
    textArea.style.top = '-9999px';
    document.body.appendChild(textArea);
    textArea.focus();
    textArea.select();

    try {
        document.execCommand('copy');
        showCopySuccess(btn);
    } catch (err) {
        btn.textContent = 'Copy failed';
        setTimeout(() => {
            btn.textContent = 'Copy to Clipboard';
        }, 2000);
    }

    document.body.removeChild(textArea);
}

function showCopySuccess(btn) {
    btn.textContent = 'Copied!';
    setTimeout(() => {
        btn.textContent = 'Copy to Clipboard';
    }, 2000);
}

function toggleEquations() {
    const content = document.getElementById('equationsContent');
    const button = document.getElementById('equationsToggle');
    const copyButton = document.getElementById('copyEquationsButton');

    if (content.style.display === 'none') {
        generateEquationsLatex();
        content.style.display = 'block';
        button.textContent = 'Hide LaTeX Equations';
        copyButton.style.display = 'inline-block';
    } else {
        content.style.display = 'none';
        button.textContent = 'Show LaTeX Equations';
        copyButton.style.display = 'none';
    }
}

function generateEquationsLatex() {
    if (!calculationResults) {
        document.getElementById('equationsCode').textContent = 'Please run calculations first.';
        return;
    }

    // Get input values
    const flowCFM = parseFloat(document.getElementById('flowRate').value);
    const dischargePSI = parseFloat(document.getElementById('dischargePressure').value);
    const efficiency = parseFloat(document.getElementById('isentropicEff').value);
    const indoorTempC = parseFloat(document.getElementById('indoorTemp').value);
    const annualHours = parseFloat(document.getElementById('annualHours').value);
    const electricRate = parseFloat(document.getElementById('electricRate').value);
    const demandRate = parseFloat(document.getElementById('demandRate').value);

    const massFlow = flowCFM * CFM_TO_KGS;
    const dischargeKpa = psiToKpa(dischargePSI);
    const indoorTempK = celsiusToKelvin(indoorTempC);

    const { baseRealPower, totals } = calculationResults;

    const latex = `\\section*{Cold Air Intake Energy Savings Calculation}

\\subsection*{System Parameters}

The compressor system operates with the following parameters:

\\begin{itemize}
    \\item Air flow rate: ${flowCFM.toFixed(0)} CFM (${massFlow.toFixed(3)} kg/s)
    \\item Discharge pressure: ${dischargePSI.toFixed(0)} PSI (${dischargeKpa.toFixed(1)} kPa)
    \\item CAGI isentropic efficiency: ${efficiency.toFixed(2)}\\%
    \\item Current indoor intake temperature: ${indoorTempC.toFixed(1)}°C (${indoorTempK.toFixed(2)} K)
    \\item Annual loaded operating hours: ${formatNumber(annualHours)} hours
\\end{itemize}

\\subsection*{Baseline Power Calculation}

The ideal compression power is calculated using the isentropic compression equation:

\\begin{equation}
W_{\\text{ideal}} = \\frac{\\gamma}{\\gamma - 1} \\times R \\times T_1 \\times \\dot{m} \\times \\left[ \\left( \\frac{P_2}{P_1} \\right)^{\\frac{\\gamma - 1}{\\gamma}} - 1 \\right]
\\label{eq:ideal-work}
\\end{equation}

where $\\gamma = ${GAMMA.toFixed(5)}$ (ratio of specific heats for air), $R = ${R_AIR.toFixed(5)}$ kJ/(kg·K) (specific gas constant for air), and atmospheric pressure $P_1 = ${P_ATM.toFixed(3)}$ kPa.

For the baseline case with indoor air at ${indoorTempK.toFixed(2)} K, the ideal compression power is ${(baseRealPower * (efficiency / 100)).toFixed(2)} kW.

The actual compressor power accounts for isentropic efficiency:

\\begin{equation}
W_{\\text{actual}} = \\frac{W_{\\text{ideal}}}{\\eta_{\\text{isentropic}}} = \\frac{${(baseRealPower * (efficiency / 100)).toFixed(2)}}{${(efficiency / 100).toFixed(4)}} = ${baseRealPower.toFixed(2)}\\text{ kW}
\\label{eq:actual-work}
\\end{equation}

\\subsection*{Monthly Energy Savings}

For each month, compression power is recalculated using the monthly average outdoor temperature. The monthly energy savings is:

\\begin{equation}
\\Delta E_{\\text{month}} = (W_{\\text{indoor}} - W_{\\text{outdoor,month}}) \\times H_{\\text{month}}
\\label{eq:monthly-energy}
\\end{equation}

where $H_{\\text{month}}$ is the compressor loaded operating hours in each month, allocated proportionally by the number of days in each month.

The total annual energy savings is:

\\begin{equation}
\\Delta E_{\\text{annual}} = \\sum_{i=1}^{12} \\Delta E_{\\text{month},i} = ${formatNumber(totals.energySavings)}\\text{ kWh}
\\label{eq:annual-energy}
\\end{equation}

\\subsection*{Demand Savings}

Monthly demand savings are calculated as the power reduction for each month:

\\begin{equation}
\\Delta kW_{\\text{month}} = W_{\\text{indoor}} - W_{\\text{outdoor,month}}
\\label{eq:monthly-demand}
\\end{equation}

The annual demand savings is the sum of all monthly demand reductions:

\\begin{equation}
\\Delta kW\\text{-months} = \\sum_{i=1}^{12} \\Delta kW_{\\text{month},i} = ${totals.deltaKW.toFixed(1)}\\text{ kW-months}
\\label{eq:annual-demand}
\\end{equation}

\\subsection*{Cost Savings}

Total annual cost savings combine energy and demand charge reductions:

\\begin{equation}
\\begin{split}
\\text{Annual Savings} &= (\\Delta E_{\\text{annual}} \\times \\text{Energy Rate}) + (\\Delta kW\\text{-months} \\times \\text{Demand Rate}) \\\\
&= (${formatNumber(totals.energySavings)} \\times \\$${electricRate.toFixed(2)}/\\text{kWh}) + (${totals.deltaKW.toFixed(1)} \\times \\$${demandRate.toFixed(2)}/\\text{kW-month}) \\\\
&= \\$${formatNumber(totals.energySavings * electricRate)} + \\$${formatNumber(totals.deltaKW * demandRate)} \\\\
&= \\$${formatNumber(totals.energySavings * electricRate + totals.deltaKW * demandRate)}
\\end{split}
\\label{eq:cost-savings}
\\end{equation}`;

    document.getElementById('equationsCode').textContent = latex;
}

function copyEquations() {
    const equationsCode = document.getElementById('equationsCode').textContent;
    const btn = document.getElementById('copyEquationsButton');

    if (navigator.clipboard && window.isSecureContext) {
        navigator.clipboard.writeText(equationsCode).then(() => {
            showCopySuccess(btn);
        }).catch(() => {
            fallbackCopy(equationsCode, btn);
        });
    } else {
        fallbackCopy(equationsCode, btn);
    }
}

// Initialize calculator on page load
document.addEventListener('DOMContentLoaded', calculate);

// Add event listeners to all inputs
document.querySelectorAll('#cold-air-calculator input').forEach(input => {
    input.addEventListener('change', calculate);
    input.addEventListener('input', calculate);
});
</script>
