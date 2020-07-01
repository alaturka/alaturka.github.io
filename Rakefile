# frozen_string_literal: true

BIN = %w[index.html].freeze

task all: %i[build lint]

desc 'Build'
task :build do
  BIN.each do |bin|
    sh "scedilla src/main.sh bin/#{bin}"
  end
end

desc 'Clean'
task :clean do
  rm_f(BIN.map { |prg| "bin/#{prg}" })
end

desc 'Lint'
task :lint do
  if ENV['lang'].nil? || ENV['lang'] == 'sh'
    sh %(shellcheck $(find -type f -and -not -path './.git/*' | xargs file --mime-type | grep text/x-shellscript$ | cut -f1 -d:)) # rubocop:disable Metrics/LineLength
  end
  sh 'markdownlint *.md' if ENV['lang'].nil? || ENV['lang'] == 'md'
end

task default: :build
