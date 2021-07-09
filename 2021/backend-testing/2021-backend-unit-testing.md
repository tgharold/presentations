# Theory

## Test Patterns

- test pyramid examples
- manual exploratory testing has value, paves the way for automated tests
- key terms, fuzziness of terms (system vs integration tests, mock vs stub vs fake)
- line coverage is not a measure of success
- cyclomatic complexity: https://en.wikipedia.org/wiki/Cyclomatic_complexity

Good book that establishes nomenclature and things to consider (not just about xUnit)

- https://www.oreilly.com/library/view/xunit-test-patterns/9780131495050/
- http://xunitpatterns.com/

## Brownfield Development

Think bit of land with nothing on it (green with shrubbery) versus a bit of land with construction underway (mostly brown mud).  There may still be parts of the land that have nothing on it where new things could be built from scratch.

Brownfield = existing code, greenfield = new projects.  But even brownfield projects can have greenfield areas.

Brownfield challenges:

- units are often tightly intertwined (logic in controllers, large numbers of dependencies)
- may require refactoring of logic into service class or static methods (less ideal)

Links:

- https://synoptek.com/insights/it-blogs/greenfield-vs-brownfield-software-development/

## TDD (Test Driven Development)

- Can be good/bad, you can delve too deep.
- Any method that makes non-trivial decisions, or which takes in multiple inputs is a candidate.
- Very useful for calculation methods (build the export filename, calculate eligibility window)
- Can encode business rules
- https://en.wikipedia.org/wiki/Test-driven_development

## BDD (Behavior driven development)

- Usually at a higher level (integration/system tests)
- Given context/inputs A, when event B occurs, then ensure C was the result
- Use to encode higher level business rules
- https://en.wikipedia.org/wiki/Behavior-driven_development

# Practicalities

## Test class structure

Where do we put the test harness code? Previously was a mish-mash of Hosts.Testing/Helpers or /TestHelpers or /Fixtures or /TestFixtures.

- Hosts.Tests/Testing
- Testing/Database folder, with Testing/Database/Tests folder
- Testing/SendGrid folder, (maybe) with Testing/SendGrid/Tests folder

## Database Fixtures

- Will be different across projects to a point
- Getting a fresh EF context can be tricky at times (IDisposable issues?)
- Often layered, with each layer having specific duties.
- RimDev.Migrations.Testing -- TestSqlClientDatabaseFixture handles creation of a test database, but goes no further.

## Object Factories

- Can be simpler in the long run for tests versus manual builds of objects (but not always)
- Can be written defensively

## How much to mock

- Any external API (carriers, SendGrid, Twilio)
- Calls to any other internal API.
- Classes that have difficult dependencies.

## Examples

- SubApi: Make_proper_decisions_for_application_user
- SubApi: Can_get_response_with_subscriberIds
- AccApi: Create_shows_that_migrations_have_run
- AccApi: SendGridClientMockFactory
- AccApi: EnhancedTwilioRestClientMockFactory