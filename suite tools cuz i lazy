import semmle.code.cpp.controlflow.ControlFlow
import semmle.code.cpp.dataflow.DataFlow

/**
 * Represents a suite of tools for starting programming.
 */
class ProgrammingSuite extends Suite {
  /**
   * Creates a new project with the given name.
   */
  predicate createProject(string projectName) {
    exists(File file |
      file.getName() = projectName + ".cpp" and
      file.getParent().isDirectory() and
      file.getParent().getName() = "projects"
    )
  }

  /**
   * Compiles the given C++ source code file.
   */
  predicate compileSource(File sourceFile) {
    exists(File objFile |
      objFile.getName() = sourceFile.getName().substringBefore(".") + ".o" and
      objFile.getParent().isDirectory() and
      objFile.getParent().getName() = "build"
    )
  }

  /**
   * Runs the tests for the given project.
   */
  predicate runTests(string projectName) {
    exists(File testFile |
      testFile.getName() = "tests.cpp" and
      testFile.getParent().isDirectory() and
      testFile.getParent().getName() = projectName
    )
  }
}

/**
 * Represents a file in the file system.
 */
class File extends Entity {
  string getName() {
    result = this.toString()
  }

  File getParent() {
    result = this
  }
}

/**
 * Entry point for the suite of programming tools.
 */
class Main {
  /**
   * Executes the specified command.
   */
  static void executeCommand(string command) {
    let cmd = command.toLowerCase().trim() |
      command = "create" |
        ProgrammingSuite.createProject(cmd.substringAfter("create").trim()) |
      command = "compile" |
        ProgrammingSuite.compileSource(File.fromString(cmd.substringAfter("compile").trim())) |
      command = "runtests" |
        ProgrammingSuite.runTests(cmd.substringAfter("runtests").trim()) |
      true
  }
}
