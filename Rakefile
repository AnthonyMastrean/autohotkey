require "rake/clean"

CLOBBER.include("**/*.exe")

SCRIPTS = FileList["**/*.ahk"]
ICONS = SCRIPTS.pathmap("%X.ico")
TARGETS = SCRIPTS.pathmap("%X.exe")

task :default => [:compile]

desc "Compile"
task :compile => TARGETS

SCRIPTS.zip(ICONS, TARGETS) do |script, icon, target|
  file target => [script] do
    File.exist?(icon) \
        ? system("ahk2exe /in \"#{script}\" /out \"#{target}\" /icon \"#{icon}\"") \
        : system("ahk2exe /in \"#{script}\" /out \"#{target}\"")
    system("mpress -q \"#{target}\"")
  end
end
