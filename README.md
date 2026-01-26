# API Integration Agent
Hands-on project for the [Building Coding Agents with Tool Execution](https://learn.deeplearning.ai/courses/building-coding-agents-with-tool-execution) course of deeplearning.ai

## Overview

This project implements an autonomous API Integration Agent capable of understanding user prompts, exploring APIs, writing client code, and executing that code within a secure sandbox environment. The agent leverages OpenAI's function calling capabilities and E2B's code interpreter sandbox to perform multi-step tasks.

## Key Features

*   **Autonomous API Interaction**: The agent can interpret a given task, identify relevant API endpoints, and construct API calls.
*   **Code Generation and Execution**: It can write and execute Python code on-the-fly to interact with APIs, process responses, and perform calculations or data manipulations.
*   **Secure Sandbox Environment**: All code execution happens within an isolated E2B sandbox, ensuring safety and preventing local system contamination.
*   **File System Interaction**: Equipped with `write_file`, `read_file`, and `list_files` tools, the agent can store API responses, configuration data, or intermediate results to the sandbox's filesystem and retrieve them as needed. This is particularly useful for handling large datasets or multi-step processing workflows.
*   **Iterative Reasoning**: The agent uses a multi-step loop, allowing it to adapt its strategy based on API responses and tool execution results, leading to more robust task completion.
*   **Flexible Tooling**: Easily extendable with new tools (e.g., for web scraping, database operations) to enhance its capabilities.

## How it Works

The agent operates on an iterative loop, following these steps:

1.  **Receives User Query**: The agent is given a task and a system prompt defining its role.
2.  **LLM Reasoning**: An OpenAI LLM processes the user query and the conversation history. Based on its understanding and the available tool schemas, it decides whether to respond directly or to call one or more tools.
3.  **Tool Execution**: If the LLM decides to call a tool (e.g., `execute_code`, `write_file`, `read_file`, `list_files`), the agent executes the corresponding function in the E2B sandbox.
    *   `execute_code`: Runs Python code (e.g., to make HTTP requests, parse JSON).
    *   `write_file`: Saves content to a specified file path within the sandbox.
    *   `read_file`: Reads the content of a file from the sandbox.
    *   `list_files`: Lists files and directories in a given path within the sandbox.
4.  **Result Integration**: The output or errors from the tool execution are captured and fed back into the LLM's conversation history.
5.  **Iteration**: The process repeats, allowing the LLM to use the new information from tool results to refine its next action, until the task is completed or a maximum number of steps is reached.
6.  **Final Response**: Once the LLM determines it has sufficient information, it provides a human-readable `FINAL` answer to the user.

## Project Structure

*   `project.ipynb`: The original Jupyter notebook showcasing the initial implementation of the API Integration Agent.
*   `project_v2.ipynb`: An enhanced version of the agent, demonstrating additional file system interaction capabilities (`read_file`, `list_files`) within the E2B sandbox to support more complex API integration workflows.
*   `requirements.txt`: Lists all Python dependencies required to run the project.
*   `docs.md`: Comprehensive documentation for `e2b-code-interpreter` and `openai` libraries, including patterns for tool execution and agent loops.

## Getting Started

To run this project, ensure you have Python installed and then set up your environment variables (`OPENAI_API_KEY`, `E2B_API_KEY`) as described in `docs.md`. Install dependencies using `pip install -r requirements.txt`. You can then open and run the `project_v2.ipynb` notebook in a Jupyter environment.
