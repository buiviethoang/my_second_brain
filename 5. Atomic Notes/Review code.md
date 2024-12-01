2024-12-01 21:22
Status: #baby
Tags: [[computer science]] [[clean code]]
## Main
- [ ] Should has README
- [ ] All source, sensible info, static data => Resources folder
- [ ] Naming convention
- [ ] Don't have any test
- [ ] Split application properties into dev, prod and test
- [ ] Good structures
- [ ] Controller
	- [ ] RequestMapping => api/v1/...
	- [ ] Should write constructor based injection instead of field injection for unit testing purposes. 
	- [ ] Should have swagger documenting
	- [ ] Write exceptions exactly where they should be. 
- [ ] DTO, Entity
	- [ ] Use the right type (Date, Money-wise)
	- [ ] Vague entity name. 
- [ ] Repo
	- [ ] Format query code.
	- [ ] Always have @Query instead of letting JPA to interprete
- [ ] Service
	- [ ] Using builder
	- [ ] Meaningful name. With good grammar. 
	- [ ] Throw right exceptions
	- [ ] Do we need Interface for service?

## References

