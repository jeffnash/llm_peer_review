# LLM Peer Review Workflow

## Overview

This project provides an interactive Python script (`run_llm_workflow.py`) to automate a peer review process between two coding LLMs (LLM A and LLM B) using the Gemini CLI. The script facilitates generating a summary of code changes by LLM A, prompting the user to get an audit from LLM B (via an external tool like Augment Code), and then processing the audit feedback to produce an updated summary. The workflow leverages the Gemini CLI to execute prompts and save outputs, ensuring a structured and systematic code review process.

The script uses two prompts:
- `llm_a_summary_prompt.txt`: Instructs LLM A to generate a detailed summary of its code changes.
- `follow_up_prompt.txt`: Instructs LLM A to analyze and incorporate feedback from LLM B’s audit.

## Prerequisites

- **Python 3.x**: Required to run the script. Ensure standard libraries (`subprocess`, `os`, `sys`, `uuid`) are available.
- **Gemini CLI**: Install via `npm install -g @google/gemini-cli` (see [Gemini CLI GitHub](https://github.com/google-gemini/gemini-cli)).
- **GEMINI_API_KEY**: Set your Gemini API key in the environment or in `~/.gemini/.env` (e.g., `GEMINI_API_KEY="YOUR_KEY"`).
- **Augment Code (or equivalent)**: A platform or tool to run LLM B’s audit prompt. Adjust instructions in the script if using a different tool.
- **Prompt Files**: Ensure `llm_a_summary_prompt.txt` and `follow_up_prompt.txt` are in the same directory as the script.

## Installation

1. Install Python 3.x if not already installed.
2. Install Gemini CLI:
   ```bash
   npm install -g @google/gemini-cli
   ```
3. Configure your Gemini credentials:
   - Run:
     ```bash
     gemini
     ```
     to set up your gemini credentials
4. Place the following files in your project directory:
   - `run_llm_workflow.py`
   - `llm_a_summary_prompt.txt`
   - `follow_up_prompt.txt`

## Usage

1. **Run the Script**:
   ```bash
   python run_llm_workflow.py
   ```

2. **Workflow Steps**:
   - The script runs the Gemini CLI with `llm_a_summary_prompt.txt` to generate LLM A’s code change summary, saved to `llm_a_summary.txt`.
   - You’ll be prompted to:
     - Open `llm_a_summary.txt` and copy its content.
     - Paste it into your audit tool (e.g., Augment Code) to run LLM B’s audit prompt.
     - Copy the audit output and paste it back into the terminal (end with Ctrl+D on Unix or Ctrl+Z on Windows).
   - The script runs the Gemini CLI again with `follow_up_prompt.txt`, incorporating the audit feedback, and saves the updated summary to `llm_a_updated_summary.txt`.

3. **Output Files**:
   - `llm_a_summary.txt`: LLM A’s initial summary of code changes.
   - `llm_a_updated_summary.txt`: LLM A’s analysis of LLM B’s audit and updated summary.

## Prompt Files

- **`llm_a_summary_prompt.txt`**: Instructs LLM A to produce a structured summary of its code changes, including an implementation plan and code diffs. This is fed to the Gemini CLI to generate `llm_a_summary.txt`.
- **`follow_up_prompt.txt`**: Instructs LLM A to analyze LLM B’s audit feedback, incorporate valid suggestions, and produce an updated summary. It includes a placeholder for the audit report and is used to generate `llm_a_updated_summary.txt`.

## Customization

- **Task-Specific Requirements**: Edit `llm_a_summary_prompt.txt` to include specific requirements or context for your coding task (e.g., replace `[insert the original requirements or problem context here]`).
- **Audit Tool**: If you’re not using Augment Code, update the script’s print statements (e.g., replace “Augment Code” with your tool’s name).
- **Gemini CLI Flags**: If your Gemini CLI setup requires different flags or commands, modify the `run_gemini_cli` function in `run_llm_workflow.py`.

## Notes

- **Error Handling**: The script checks for Gemini CLI installation, file existence, and CLI errors. It prompts for API key setup if needed.
- **User Interaction**: Paste the audit report in the terminal, ending with Ctrl+D (Unix) or Ctrl+Z (Windows).
- **Security**: Keep your `GEMINI_API_KEY` secure and avoid exposing it in shared environments.
- **Limitations**: The script assumes the Gemini CLI supports `-p` for prompts and `-o` for output files. If your CLI version differs, adjust the `run_gemini_cli` function.

## Example Workflow

1. Run `python run_llm_workflow.py`.
2. The script generates `llm_a_summary.txt` using `llm_a_summary_prompt.txt`.
3. Copy the content of `llm_a_summary.txt` and paste it into your audit tool to get LLM B’s audit report.
4. Paste the audit report into the terminal when prompted.
5. The script generates `llm_a_updated_summary.txt` with LLM A’s revised summary based on the audit.

## Troubleshooting

- **Gemini CLI Not Found**: Ensure it’s installed (`npm install -g @google/gemini-cli`) and in your PATH.
- **File Errors**: Ensure `llm_a_summary_prompt.txt` and `follow_up_prompt.txt` are in the same directory as the script.
- **Audit Input Issues**: Paste the full audit report and end with Ctrl+D/Ctrl+Z to avoid errors.

## License

MIT License. See [LICENSE](LICENSE) for details.
