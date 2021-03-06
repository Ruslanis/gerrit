load('//tools/bzl:junit.bzl', 'junit_tests')

DEPS = [
  '//gerrit-common:server',
  '//gerrit-extension-api:api',
  '//gerrit-reviewdb:server',
  '//gerrit-server:server',
  '//lib:guava',
  '//lib:gwtorm',
  '//lib/guice:guice',
  '//lib/guice:guice-assistedinject',
  '//lib/guice:guice-servlet',
  '//lib/jgit/org.eclipse.jgit:jgit',
  '//lib/log:api',
]

java_library(
  name = 'gpg',
  srcs = glob(['src/main/java/**/*.java']),
  deps = DEPS + [
    '//lib/bouncycastle:bcpg',
    '//lib/bouncycastle:bcprov',
  ],
  visibility = ['//visibility:public'],
)

TESTUTIL_SRCS = glob(['src/test/**/testutil/**/*.java'])

java_library(
  name = 'testutil',
  srcs = TESTUTIL_SRCS,
  deps = DEPS + [
    ':gpg',
    '//lib/bouncycastle:bcpg-without-neverlink',
    '//lib/bouncycastle:bcprov-without-neverlink',
  ],
  visibility = ['//visibility:public'],
)

junit_tests(
  name = 'gpg_tests',
  srcs = glob(
    ['src/test/java/**/*.java'],
    exclude = TESTUTIL_SRCS,
  ),
  deps = DEPS + [
    ':gpg',
    ':testutil',
    '//gerrit-cache-h2:cache-h2',
    '//gerrit-lucene:lucene',
    '//gerrit-server:testutil',
    '//lib:truth',
    '//lib/jgit/org.eclipse.jgit.junit:junit',
    '//lib/bouncycastle:bcpg-without-neverlink',
    '//lib/bouncycastle:bcprov-without-neverlink',
  ],
  visibility = ['//visibility:public'],
)
