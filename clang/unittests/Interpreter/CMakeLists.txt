set(LLVM_LINK_COMPONENTS
  ${LLVM_TARGETS_TO_BUILD}
  Core
  OrcJIT
  Support
  TargetParser
  )

add_clang_unittest(ClangReplInterpreterTests
  IncrementalCompilerBuilderTest.cpp
  IncrementalProcessingTest.cpp
  InterpreterTest.cpp
  CodeCompletionTest.cpp
  )
target_link_libraries(ClangReplInterpreterTests PUBLIC
  clangAST
  clangBasic
  clangInterpreter
  clangFrontend
  clangSema
  )

# Exceptions on Windows are not yet supported.
if(NOT WIN32)
  add_subdirectory(ExceptionTests)
endif()

export_executable_symbols(ClangReplInterpreterTests)
